# HM Land Registry (hm-land-registry)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

HM Land Registry is the non-ministerial government department that registers the ownership of land and property in England and Wales, guaranteeing title to more than 26 million registered estates. In a United Kingdom market that has no MLS and no cooperative listing standard — residential listings are controlled by the Rightmove and Zoopla duopoly and reach them through agency CRM software — HMLR is the counterweight, and it sits at the legal foundation of the value chain rather than at the consumer end: it is the authoritative source of who owns what, what it sold for, and where its boundaries are, and every conveyancing transaction in England and Wales terminates at its register. Its API posture is genuinely and unusually good for a registry, but it is split into three tiers that should never be conflated. First, a real open layer: the landregistry.data.gov.uk platform serves a live, anonymous, unauthenticated SPARQL 1.1 endpoint plus a W3C Linked Data API over Price Paid Data and the UK House Price Index, with JSON/CSV/Turtle content negotiation, alongside bulk Price Paid CSVs and INSPIRE index polygons — all under the Open Government Licence v3.0 with no signup, no key and no fee. Second, a self-serve keyed tier: the Use land and property data service issues an API key automatically on account creation and exposes a documented REST API for dataset metadata and signed download URLs, but the datasets behind it require a signed licence per dataset and some are chargeable — the Registered Leases commercial licence is £5,000 a year plus VAT, and the National Polygon Service, which holds the title boundary polygons and the title number to UPRN lookup, is £20,000 a year plus VAT. A state registry selling the spatial extent of the public record back to the public is the finding, and it is recorded here plainly. Third, the Business Gateway: the B2B channel that conveyancers and their case management systems use to submit applications to change the register, order official copies and run priority searches. Its developer pack is fully public on GitHub Pages with eight downloadable OpenAPI 3.0/3.1 contracts and 37 SOAP XSDs, but the production host businessgateway.landregistry.gov.uk will not complete a TLS handshake without an HMLR-issued client certificate, and access requires signing a development licence and holding a business e-services account. There is no RESO Web API certification, no RESO Data Dictionary, no OData $metadata document and no Universal Property Identifier anywhere in HMLR's stack — RESO is a North American NAR construct with no UK adoption, and HMLR's machine-readable contracts are OpenAPI, XSD and W3C linked data instead.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/hm-land-registry/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/hm-land-registry/refs/heads/main/apis.yml)

## Tags

- Real Estate
- United Kingdom
- Land Registry
- Open Data
- Title
- Conveyancing
- Property Records
- Price Paid Data
- Linked Data
- Geospatial
- Government
- PropTech

## Timestamps

- **Created:** 2026-07-26
- **Modified:** 2026-07-26

## APIs

### HM Land Registry Open Data SPARQL API

Live SPARQL 1.1 query endpoint over HM Land Registry's open linked data — Price Paid Data transaction records for every property sale in England and Wales lodged for registration, and the UK House Price Index. Callable anonymously with no API key, no account and no licence signature; verified returning HTTP 200 with application/sparql-results+json on 2026-07-26. Results are available as table, plain text, JSON and XML. Published under the Open Government Licence v3.0 with a required Crown copyright attribution statement.

- **Human URL:** [http://landregistry.data.gov.uk/qonsole](http://landregistry.data.gov.uk/qonsole)
- **Base URL:** `https://landregistry.data.gov.uk/landregistry/query`

#### Tags

- Open Data
- SPARQL
- Linked Data
- Price Paid Data
- United Kingdom

#### Properties

- [Documentation](http://landregistry.data.gov.uk/qonsole)
- [Documentation](https://www.gov.uk/land-registry-public-data)
- [Documentation](https://landregistry.data.gov.uk/def/ppi)
- [Documentation](https://landregistry.data.gov.uk/def/common)
- [TermsOfService](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)

### HM Land Registry Price Paid Data Linked Data API

W3C Linked Data API over the Price Paid Data dataset, exposing every property sale in England and Wales sold for value and lodged for registration since 1995. Resources resolve at /data/ppi/ with content negotiation by file extension (.json, .csv, .ttl, .rdf) and standard Linked Data API paging parameters such as _pageSize and _page. No authentication of any kind is required; verified HTTP 200 anonymously on 2026-07-26. Bulk yearly and complete CSV files are also published on the price-paid-data.publicdata host. Open Government Licence v3.0.

- **Human URL:** [http://landregistry.data.gov.uk/app/ppd/](http://landregistry.data.gov.uk/app/ppd/)
- **Base URL:** `https://landregistry.data.gov.uk/data/ppi`

#### Tags

- Open Data
- Linked Data
- Price Paid Data
- Transactions
- United Kingdom

#### Properties

- [Documentation](http://landregistry.data.gov.uk/app/ppd/)
- [Documentation](https://www.gov.uk/guidance/about-the-price-paid-data)
- [Documentation](https://landregistry.data.gov.uk/def/ppi)
- [BulkData](https://www.gov.uk/government/statistical-data-sets/price-paid-data-downloads)
- [BulkData](https://price-paid-data.publicdata.landregistry.gov.uk/pp-complete.csv)
- [TermsOfService](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)

### UK House Price Index Linked Data API

W3C Linked Data API over the UK House Price Index, the official house price statistic calculated by the Office for National Statistics from HM Land Registry, Registers of Scotland and Land and Property Services Northern Ireland sales data. Region and month resources resolve at /data/ukhpi/ with .json, .csv and .ttl representations carrying average price, index and percentage change broken out by property type, buyer type, funding type and new-build status. Anonymous, no key; verified HTTP 200 on 2026-07-26. Open Government Licence v3.0.

- **Human URL:** [http://landregistry.data.gov.uk/app/ukhpi/](http://landregistry.data.gov.uk/app/ukhpi/)
- **Base URL:** `https://landregistry.data.gov.uk/data/ukhpi`

#### Tags

- Open Data
- Linked Data
- Valuation
- Statistics
- United Kingdom

#### Properties

- [Documentation](http://landregistry.data.gov.uk/app/ukhpi/)
- [Documentation](https://landregistry.data.gov.uk/app/ukhpi/doc/ukhpi-user-guide)
- [Documentation](https://www.gov.uk/government/collections/uk-house-price-index-reports)
- [TermsOfService](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)

### Use Land and Property Data API

RESTful JSON API for the Use land and property data service, used to list the HM Land Registry bulk datasets available in the service, read dataset metadata and resources, and mint a signed S3 download URL valid for 10 seconds for a named file or historical file. Datasets reachable through it include UK companies that own property in England and Wales (CCOD), Overseas companies that own property in England and Wales (OCOD), the National Polygon Service, Restrictive Covenants and Registered Leases. Authentication is an API key sent in the Authorization header, issued automatically on self-serve account creation — but every download endpoint additionally requires that you have signed the licence for that specific dataset and, where the dataset is chargeable, paid for it. Called anonymously on 2026-07-26 it returns HTTP 403 with "Access denied: You need to provide your API Key to perform this operation".

- **Human URL:** [https://use-land-property-data.service.gov.uk/api-information](https://use-land-property-data.service.gov.uk/api-information)
- **Base URL:** `https://use-land-property-data.service.gov.uk/api/v1`

#### Tags

- Open Data
- Bulk Data
- Property Records
- Ownership
- United Kingdom

#### Properties

- [Documentation](https://use-land-property-data.service.gov.uk/api-information)
- [APIReference](https://use-land-property-data.service.gov.uk/api-documentation)
- [SignUp](https://use-land-property-data.service.gov.uk/registration)
- [TermsOfService](https://use-land-property-data.service.gov.uk/service-terms-of-use)
- [Support](https://use-land-property-data.service.gov.uk/contact)

### Business Gateway Submit an Application to Change the Land Register API

The Business Gateway REST API through which conveyancers and their case management systems lodge applications to change the land register, upload and download supporting documents, add attachments and messages to a lodged application, and poll and acknowledge asynchronous outcome notifications. Two OpenAPI contracts are published and harvested here — v0.3 (OpenAPI 3.0.1, six operations on /v0) and v1.0 (OpenAPI 3.1.0, spec version 1.0.5, ten operations on /v1). A v1.1 directory exists in the developer pack but both openapi.json and openapi.html in it are zero-byte placeholders, so nothing was saved for it. Security is HTTP Basic over mutual TLS with an HMLR-issued client certificate.

- **Human URL:** [https://landregistry.github.io/bgtechdoc/rest/get_started/developer_guide/index.html](https://landregistry.github.io/bgtechdoc/rest/get_started/developer_guide/index.html)
- **Base URL:** `https://businessgateway.landregistry.gov.uk/bg2/api`

#### Tags

- Conveyancing
- Title
- Land Registry
- Applications
- United Kingdom

#### Properties

- [OpenAPI](openapi/hm-land-registry-submit-application-to-change-the-register-v1.0-openapi.json)
- [OpenAPI](openapi/hm-land-registry-submit-application-to-change-the-register-v0.3-openapi.json)
- [JSONSchema](json-schema/hm-land-registry-application-completed.json)
- [JSONSchema](json-schema/hm-land-registry-application-accepted-priority-pending.json)
- [JSONSchema](json-schema/hm-land-registry-application-accepted-priority-protected.json)
- [JSONSchema](json-schema/hm-land-registry-application-cancelled.json)
- [JSONSchema](json-schema/hm-land-registry-application-correspondence-despatched.json)
- [JSONSchema](json-schema/hm-land-registry-application-validation-failed.json)
- [JSONSchema](json-schema/hm-land-registry-application-attachment-success.json)
- [JSONSchema](json-schema/hm-land-registry-application-attachment-failed.json)
- [JSONSchema](json-schema/hm-land-registry-application-message-success.json)
- [JSONSchema](json-schema/hm-land-registry-application-message-failed.json)
- [JSONSchema](json-schema/hm-land-registry-application-error.json)
- [Documentation](https://landregistry.github.io/bgtechdoc/)
- [Authentication](https://landregistry.github.io/bgtechdoc/rest/get_started/developer_guide/index.html)

### Business Gateway Official Search of Whole (with Priority) with Data API

RESTful expansion of the long-standing Official Search of Whole SOAP service. An official search with priority by a purchaser against the whole of a registered title or a pending first registration application, protecting the agreement between buyer, seller and lender for the priority period. Single POST operation on /v1/official-searches-of-whole, described by an OpenAPI 3.1.0 document that declares both the test host bgtest.landregistry.gov.uk and the production host businessgateway.landregistry.gov.uk.

- **Human URL:** [https://landregistry.github.io/bgtechdoc/services/official_search_of_whole_rest/](https://landregistry.github.io/bgtechdoc/services/official_search_of_whole_rest/)
- **Base URL:** `https://businessgateway.landregistry.gov.uk/bg2/api`

#### Tags

- Conveyancing
- Title
- Search
- United Kingdom

#### Properties

- [OpenAPI](openapi/hm-land-registry-official-search-of-whole-with-data-openapi.yml)
- [Documentation](https://landregistry.github.io/bgtechdoc/services/official_search_of_whole_rest/)
- [Documentation](https://landregistry.github.io/bgtechdoc/rest/get_started/developer_guide/index.html)

### Business Gateway Official Copy Document Availability Service

Returns OC1 document availability (title register and title plan) and a collection of OC2 document availability (documents referred to in the register) for a given title number, so a case management system can tell a conveyancer what official copies can actually be ordered before ordering them. Two OpenAPI 3.0.0 contracts are published and harvested — v1 on /bg2/api/v1 and v2 on /bg2/api/v2 — both securing the single GET operation with HTTP Basic.

- **Human URL:** [https://landregistry.github.io/bgtechdoc/services/official_copy_document_availability_v2/](https://landregistry.github.io/bgtechdoc/services/official_copy_document_availability_v2/)
- **Base URL:** `https://businessgateway.landregistry.gov.uk/bg2/api/v2`

#### Tags

- Conveyancing
- Title
- Documents
- United Kingdom

#### Properties

- [OpenAPI](openapi/hm-land-registry-official-copy-document-availability-v2-openapi.json)
- [OpenAPI](openapi/hm-land-registry-official-copy-document-availability-v1-openapi.json)
- [Documentation](https://landregistry.github.io/bgtechdoc/services/official_copy_document_availability_v2/)
- [Documentation](https://landregistry.github.io/bgtechdoc/services/official_copy_document_availability_v1/)

### Business Gateway Registered Proprietor Names Service

Returns the registered proprietor names recorded against a supplied title number — the authoritative answer to "who owns this". Single GET operation on /titles/{title_number}/registered-proprietor-names described by an OpenAPI 3.0.0 document declaring both the production and bgtest hosts and securing the operation with HTTP Basic over mutual TLS.

- **Human URL:** [https://landregistry.github.io/bgtechdoc/services/registered_proprietor_names/](https://landregistry.github.io/bgtechdoc/services/registered_proprietor_names/)
- **Base URL:** `https://businessgateway.landregistry.gov.uk/bg2/api/v1`

#### Tags

- Title
- Ownership
- Property Records
- United Kingdom

#### Properties

- [OpenAPI](openapi/hm-land-registry-registered-proprietor-names-openapi.json)
- [Documentation](https://landregistry.github.io/bgtechdoc/services/registered_proprietor_names/)

### Business Gateway Estimate Completion Date API

Returns HM Land Registry's estimated completion date for a lodged application, given its application reference, so a conveyancer's system can set client expectations on how long a registration will take. Single GET operation on /v1/applications/{application_reference}/estimate-completion-date, OpenAPI 3.0.0, HTTP Basic, with both the production and bgtest hosts declared.

- **Human URL:** [https://landregistry.github.io/bgtechdoc/services/estimated_completion_date/](https://landregistry.github.io/bgtechdoc/services/estimated_completion_date/)
- **Base URL:** `https://businessgateway.landregistry.gov.uk/bg2/api`

#### Tags

- Conveyancing
- Applications
- United Kingdom

#### Properties

- [OpenAPI](openapi/hm-land-registry-estimate-completion-date-openapi.yml)
- [Documentation](https://landregistry.github.io/bgtechdoc/services/estimated_completion_date/)

### Land Register API

An OpenAPI 3.0.1 contract, version 6.0.0, titled "Land Register API" and published in the public Business Gateway developer pack. It describes two GET operations — /title/{titleNumber} and /draft-titles/{titleNumber} — and states that it "aims to be the primary method of accessing register data for HM Land Registry". No baseURL is recorded here because the specification declares no public production server: its servers list contains only localhost ports and internal HMLR hosts under development, test and *.stp.hmlr.zone. Access is not a developer product at all — it must be requested through the Digital Register project team, an individual bearer token is minted per consuming service, and the consumer must file a Fraud Impact Assessment and must not expose the data externally. Recorded as a real published contract for an internal government API, not as a callable public API.

- **Human URL:** [https://landregistry.github.io/bgtechdoc/](https://landregistry.github.io/bgtechdoc/)

#### Tags

- Title
- Property Records
- Land Registry
- Internal
- United Kingdom

#### Properties

- [OpenAPI](openapi/hm-land-registry-land-register-api-openapi.yml)
- [OpenAPI](https://landregistry.github.io/bgtechdoc/documents/openapi.yaml)
- [Documentation](https://landregistry.github.io/bgtechdoc/)

## Common Properties

- [Website](https://www.gov.uk/government/organisations/land-registry)
- [Documentation](https://landregistry.github.io/bgtechdoc/)
- [Documentation](https://use-land-property-data.service.gov.uk/api-information)
- [APIReference](https://use-land-property-data.service.gov.uk/api-documentation)
- [Authentication](https://landregistry.github.io/bgtechdoc/rest/get_started/developer_guide/index.html)
- [OpenData](https://landregistry.data.gov.uk/)
- [OpenData](https://www.gov.uk/land-registry-public-data)
- [BulkData](https://www.gov.uk/government/statistical-data-sets/price-paid-data-downloads)
- [TermsOfService](https://use-land-property-data.service.gov.uk/service-terms-of-use)
- [License](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)
- [SignUp](https://use-land-property-data.service.gov.uk/registration)
- [Onboarding](https://www.gov.uk/guidance/direct-integration-with-business-gateway)
- [Onboarding](https://www.gov.uk/guidance/hm-land-registry-business-gateway)
- [DeveloperPack](https://www.gov.uk/guidance/business-gateway-developer-pack)
- [GitHubOrganization](https://github.com/LandRegistry)
- [SourceCode](https://github.com/LandRegistry/bgtechdoc)
- [Glossary](https://landregistry.github.io/bgtechdoc/support/glossary/)
- [Support](https://use-land-property-data.service.gov.uk/contact)
- [Accessibility](https://use-land-property-data.service.gov.uk/accessibility-statement)

## Maintainers

- Kin Lane — kin@apievangelist.com
