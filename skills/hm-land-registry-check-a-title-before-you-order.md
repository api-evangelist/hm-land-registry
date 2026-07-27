---
name: Check a title before you order
description: >-
  Establish who owns a registered title and what official copies can actually be
  ordered for it, before spending money ordering them. Read-only.
api: openapi/hm-land-registry-registered-proprietor-names-openapi.json
operations:
  - getRegisteredProprietorNames
  - getOfficialCopiesAvailability
  - getEstimateCompletionDate
generated: '2026-07-26'
method: generated
---

# Check a title before you order

Three cheap read-only Business Gateway calls that de-risk a conveyancing file. All three need the HMLR-issued client certificate for mutual TLS plus HTTP Basic credentials; none of them changes anything.

## Steps

1. **Confirm ownership.** Call `getRegisteredProprietorNames` (`GET /titles/{title_number}/registered-proprietor-names` on `/bg2/api/v1`). This is the authoritative answer to "who owns this" — the registered proprietor names and types recorded against the title. Run it at instruction and again before submission; a change between the two is the signal that matters.

2. **Check what copies exist.** Call `getOfficialCopiesAvailability` (`GET /titles/{title_number}/official-copies/availability` on `/bg2/api/v2`). It returns OC1 availability (the title register and title plan) and a collection of OC2 availability (documents referred to in the register). Use it to tell a conveyancer what can actually be ordered *before* ordering. Bind to v2; v1 remains published on `/bg2/api/v1` with the same operationId, and both also ship customer-test contracts pointing at `bgtest.landregistry.gov.uk`.

3. **Set expectations on a lodged application.** If you already have an application in flight, call `getEstimateCompletionDate` (`GET /v1/applications/{application_reference}/estimate-completion-date`) for HMLR's estimate of when the registration will complete.

## Error handling

All three return 400 "Invalid request" for a malformed title number and 404 "Title not found" where the title is not registered or not visible to you. Estimate Completion Date collapses everything into a single `4XX` range response rather than enumerating statuses, so branch on the status code you actually receive, not on a documented list. See `errors/hm-land-registry-problem-types.yml`.

## Note on the internal Land Register API

The developer pack also publishes a `Land Register API` contract (`getTitle`, `getDraftTitle`) which describes itself as "the primary method of accessing register data". Do not build against it. Its `servers` block contains only localhost and internal `*.stp.hmlr.zone` hosts, access must be requested from the Digital Register project team, a bearer token is minted per consuming service, the consumer must file a Fraud Impact Assessment, and the data must not be exposed externally. It is a real published contract for an internal government API, not a developer product.
