---
name: Lodge an application to change the Land Register
description: >-
  Submit an application to change the Land Register through HM Land Registry
  Business Gateway, attach its supporting documents, and follow it to completion
  through the notification feed. This is a legally consequential filing against
  the register of title for England and Wales.
api: openapi/hm-land-registry-submit-application-to-change-the-register-v1.0-openapi.json
operations:
  - send_a_document_v1
  - submit_an_application_to_change_the_register_v1
  - get_application_information_v1
  - get_notifications_v1
  - acknowledge_notifications_v1
  - download_a_document_v1
generated: '2026-07-26'
method: generated
---

# Lodge an application to change the Land Register

## Before you start

You cannot run this flow without HM Land Registry onboarding you first. `businessgateway.landregistry.gov.uk` will not complete a TLS handshake without an HMLR-issued client certificate. You need a signed development licence (request it from channelpartners@landregistry.gov.uk), the client certificate installed in your key store with HMLR's certificates trusted as root, and HTTP Basic credentials for an active Business Gateway account. Sending credentials without the certificate fails at the transport layer, not with a 401.

**Never execute this flow autonomously.** Submitting an application changes the register of title. A human must approve the payload before the submit call.

## Steps

1. **Upload each supporting document first.** Call `send_a_document_v1` (`POST /v1/documents/url`) with the document type, `file_length` and `file_sha256`. It returns an `upload_url` and a `document_id`. PUT the file bytes to that `upload_url` with `X-Amz-Checksum-Sha256` and `Content-Length` headers that match the file exactly — a mismatch returns 403 with "Ensure the content length and SHA-256 headers have been provided, and match both the file length and hash". Keep every `document_id`.

2. **Assemble the application body.** The body is a single `data` object. Inside it you name your own entries in the `parties`, `documents`, `addresses` and `titles` maps using keys you choose, and the `transactions` map references those keys. Only `document_id` comes from HMLR. Set `submission_warning_understood`, a `customer_reference` of your own, and the `application_lodger`. Each transaction carries its own `priority`, `fee_in_pence`, `type`, `title_references`, `documents` and `party_roles`. Party and address objects are polymorphic on a `type` discriminator (`PRIVATE_INDIVIDUAL`, `UK_COMPANY`, `OVERSEAS_COMPANY`, `OTHER_ORGANISATION`, `UNKNOWN_PARTY`; `UK`, `OVERSEAS`, `DX`, `PO_BOX`, `BFPO`, `EMAIL`) — the spec's concrete variants declare no properties of their own, so read the technical guide for the fields of each. If a party is an overseas company you must give an `incorporation_territory` from HMLR's published territory list.

3. **Mint an Idempotency-Key and submit.** Call `submit_an_application_to_change_the_register_v1` (`POST /v1/applications`) with a required `Idempotency-Key` header. A successful call returns 202 with `data.application_request_id`. Store it — it is the key for every later step and appears as `subject` on every notification about this application.

4. **Retry correctly, or not at all.** Retry only on 408, 429, 500–599 and network timeouts, and only with the *same* key and *unchanged* data. If the original succeeded but the response timed out, the retry is treated as a duplicate: your payload is ignored and the original `application_request_id` comes back — that is the correct outcome, not an error. Do not retry 401 or 403; those mean your credentials or permissions are wrong. If you change the payload for any reason, including to fix a validation error, that is a new request and needs a **new** key.

5. **Expect validation to arrive later.** Only schema violations come back synchronously as 400. Every other validation failure arrives asynchronously as an `application.validation-failed` notification. Do not treat a 202 as acceptance.

6. **Poll the notification feed.** Call `get_notifications_v1` (`GET /v1/notifications`). Filter with `created_after` or `occurred_after` to advance; a call with no parameters returns the 100 oldest. Watch for `application.accepted-priority-pending` (queuing for the daylist), `application.accepted-priority-protected` (on the daylist, carrying the priority timestamp and `hmlr_reference`), `application.validation-failed`, `application.error`, `application.correspondence-despatched`, `application.cancelled` and `application.completed`.

7. **Deduplicate.** Delivery is at least once. Two notifications with the same `event_datetime` and `notification_type` but different `notification_id`s are the same event. Process one, but acknowledge both.

8. **Acknowledge everything you process.** Call `acknowledge_notifications_v1` (`POST /v1/notifications/acknowledge`) with `{"data": ["<notification_id>", …]}`. Unacknowledged notifications keep coming back forever — until the one-month deletion window, after which they are gone whether acknowledged or not. Do not rely on the feed as long-term storage.

9. **Fetch detail when a notification is thin.** Most notification payloads carry only a status. Call `get_application_information_v1` (`GET /v1/applications/{application_request_id}/information`) for the full picture: `status`, `priority_timestamp`, `hmlr_reference`, `errors`, `warnings` and `correspondences`. Note it does not currently return information about attachments, messages or early completion.

10. **Collect correspondence.** `application.correspondence-despatched`, `application.cancelled` and `application.completed` carry a list of documents with `download_id`s. Call `download_a_document_v1` (`GET /v1/documents/{document_id}`), which returns a 302 to a short-lived URL — follow it immediately. This is the only operation in the estate that declares 429, so back off if you hit one.

## Error handling

Reference: `errors/hm-land-registry-problem-types.yml`. Note the estate does not use one error format: `get_notifications_v1` and `acknowledge_notifications_v1` return RFC 9457 `application/problem+json`, `download_a_document_v1` offers it alongside `application/json`, and the rest of the flow uses a bespoke `errors` envelope. A 404 from `get_application_information_v1`, `attach_a_document_v1` or `attach_a_message_v1` means the `application_request_id` is unknown to the system.

## Testing

There is no self-serve sandbox. HMLR publishes static test stubs with four scenarios at `https://bgtest.landregistry.gov.uk/bg2test/api`; against them `Authorization` and `Idempotency-Key` accept any value and key uniqueness is not enforced, so the stubs will not catch an idempotency bug. See `sandbox/hm-land-registry-sandbox.yml`.
