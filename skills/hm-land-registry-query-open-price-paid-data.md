---
name: Query open Price Paid Data and the House Price Index
description: >-
  Query HM Land Registry's open linked-data platform for property sale prices and
  the UK House Price Index. Anonymous, free, no key and no account.
api: apis.yml#hm-land-registry-open-data-sparql-api
operations:
  - SPARQL 1.1 query
  - Linked Data API resource resolution
generated: '2026-07-26'
method: generated
---

# Query open Price Paid Data and the House Price Index

This is the one HM Land Registry surface an agent can use immediately. No key, no account, no licence signature, no client certificate. Everything below was verified returning HTTP 200 anonymously on 2026-07-26.

## What is here

- **Price Paid Data** — every property sale in England and Wales sold for value and lodged for registration since 1995.
- **UK House Price Index** — the official house price statistic, calculated by the Office for National Statistics from HM Land Registry, Registers of Scotland and Land and Property Services Northern Ireland data, broken out by property type, buyer type, funding type and new-build status.

## Steps

1. **Explore interactively first.** The Qonsole console at `http://landregistry.data.gov.uk/qonsole` is a live in-browser SPARQL playground with worked example queries. Start there before writing code.

2. **Learn the vocabulary.** The ontologies are published and harvested into this repo: `vocabulary/hm-land-registry-ppi.ttl` (Price Paid: `ppi:Transaction`, `ppi:TransactionRecord`, `ppi:RecordStatusConcept`), `vocabulary/hm-land-registry-common.ttl` and `vocabulary/hm-land-registry-ukhpi.ttl`. Bind the prefixes `ppi:` to `http://landregistry.data.gov.uk/def/ppi/` and `common:` to `http://landregistry.data.gov.uk/def/common/`. Do not guess predicate names — read the ontology.

3. **Query with SPARQL.** POST or GET your SPARQL 1.1 query to `https://landregistry.data.gov.uk/landregistry/query`. Ask for `application/sparql-results+json`; table, plain text, JSON and XML are all available.

4. **Or resolve resources directly.** The W3C Linked Data API is often simpler than SPARQL for straightforward lookups. Price Paid resources resolve under `https://landregistry.data.gov.uk/data/ppi` and House Price Index resources under `https://landregistry.data.gov.uk/data/ukhpi`. Select the representation with a file extension (`.json`, `.csv`, `.ttl`, `.rdf`) and page with `_page` and `_pageSize`.

5. **Go bulk when the query is large.** For anything approaching a full scan, do not hammer the endpoint — download the published CSVs instead: yearly and complete files at `https://www.gov.uk/government/statistical-data-sets/price-paid-data-downloads`, including `pp-complete.csv` from `price-paid-data.publicdata.landregistry.gov.uk`.

6. **Attribute.** Everything here is Open Government Licence v3.0 and the attribution statement is a licence condition, not a courtesy. Carry "Contains HM Land Registry data © Crown copyright and database right" wherever you present the data.

## What this data cannot tell you

Price Paid Data is keyed on the address, not on the title number, and it records sales — not ownership. It will not tell you who owns a property today, it will not give you a boundary, and there is no free join from an address or UPRN to a title number. The title-number-to-UPRN lookup and the boundary polygons live in the National Polygon Service, which is a chargeable dataset behind the Use land and property data service at £20,000 a year plus VAT. Current ownership is a Business Gateway question (`getRegisteredProprietorNames`), not an open-data one.

## No rate limits are published

There is no documented rate limit or quota on the open estate. Be a good citizen: cache, page, and prefer the bulk files over repeated large queries.
