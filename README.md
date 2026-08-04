# RE/MAX (re-max)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

RE/MAX Holdings, Inc. (NYSE: RMAX, SIC 6531, Denver, Colorado) is one of the world's largest real estate brokerage franchisors, licensing the RE/MAX brand to independently owned and operated brokerages across more than 110 countries and territories, and franchising mortgage brokerages in the United States under the Motto Mortgage brand with loan processing through wemlo. Its home market is the United States, where it sits in the value chain as a franchisor and consumer portal operator rather than as a data owner: the listing content behind remax.com is licensed from roughly 500 local Multiple Listing Services under IDX and syndication agreements, so RE/MAX is a consumer of MLS data, not a publisher of it. Its API posture reflects that position honestly. RE/MAX is a RESO Class D member (Brokers, Agents and Appraisers) and holds a seat on the RESO Board of Directors, but it does not appear in the RESO certification directory of certified data providers and publishes no RESO Web API, no OData `$metadata` document and no Universal Property Identifier surface. In the United States there is no developer portal, no published API program and no machine-readable contract of any kind; `developer.remax.com`, `developers.remax.com` and `docs.remax.com` are only wildcard DNS entries pointing at the kvCORE agent website platform, and `api.remax.com` is a dangling CNAME to a decommissioned booj host that no longer resolves. The only real, publicly documented RE/MAX API surface belongs to RE/MAX Europe, whose Datahub franchise-operations API and Listings API are published as public Postman documentation with OAuth 2.0 authentication, but whose credentials are issued only to RE/MAX regional master franchisees, offices and their vendors — documented, but not self-serve.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/re-max/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/re-max/refs/heads/main/apis.yml)

## Tags

- Real Estate
- United States
- Brokerage
- Property Listings
- MLS
- RESO
- IDX
- PropTech
- Franchising
- Mortgage
- Rentals

## Timestamps

- **Created:** 2026-07-26
- **Modified:** 2026-07-26

## APIs

### RE/MAX Europe Datahub API

The RE/MAX Europe Datahub API is the franchise-operations API behind the RE/MAX EU Datahub application. It exposes offices, persons, RE/MAX Titles (the agent/broker role records), teams, regions and monthly GCI / transaction / volume reporting to RE/MAX regional master franchisees and their vendors. It is a proprietary REST contract — it carries no RESO Data Dictionary fields, no OData surface and no Universal Property Identifier. Authentication is OAuth 2.0 against `https://oauth.datahub.remax.eu`, with the resulting token passed as an `access_token` query parameter; the published Postman documentation carries the client_id placeholder `Ask_REU`, confirming credentials are handed out by RE/MAX Europe rather than self-served. Documentation is public; access is not.

- **Human URL:** [https://apidocs.datahub.remax.eu/](https://apidocs.datahub.remax.eu/)
- **Base URL:** `https://api.datahub.remax.eu/external`

#### Tags

- Franchising
- Offices
- Agents
- Teams
- Reporting
- Europe

#### Properties

- [Documentation](https://apidocs.datahub.remax.eu/)
- [Postman Collection](collections/re-max-eu-datahub-api.postman_collection.json) — [Postman Collection 2.0](https://schema.getpostman.com/json/collection/v2.0.0/collection.json)
- [Authentication](https://oauth.datahub.remax.eu/authorize)

### RE/MAX Europe Listings API

The RE/MAX Europe Listings API is used in conjunction with the RE/MAX EU Datahub application to add, update, retrieve and delete property listing data and listing images across RE/MAX European regions. It exposes listings, listing images, listing entry logs, regions, offices and agents, plus convenience reads for listing countries and cities by country. Writes go through a queue with deferred validation. Like the Datahub API it is a proprietary REST schema with no RESO Data Dictionary alignment, no OData `$metadata` and no UPI. Authentication is OAuth 2.0 with the token supplied as an `access_token` query parameter. The only public documentation RE/MAX Europe publishes is for the STAGING environment, whose endpoints run on a third-party host (`bwscloud.tech`); no production base URL is published.

- **Human URL:** [https://listingsapi-test.datahub.remax.eu/](https://listingsapi-test.datahub.remax.eu/)
- **Base URL:** `https://listing-api-remaxeu.bwscloud.tech/api/v1`

#### Tags

- Property Listings
- Images
- Regions
- Agents
- Europe
- Staging

#### Properties

- [Documentation](https://listingsapi-test.datahub.remax.eu/)
- [Postman Collection](collections/re-max-eu-listings-api.postman_collection.json) — [Postman Collection 2.0](https://schema.getpostman.com/json/collection/v2.0.0/collection.json)

## Common Properties

- [Website](https://www.remax.com/)
- [Website](https://www.remax.eu/)
- [Blog](https://news.remax.com/)
- [Investor Relations](https://investors.remaxholdings.com/)
- [LinkedIn](https://www.linkedin.com/company/remax)
- [Documentation](https://apidocs.datahub.remax.eu/)
- [Authentication](https://oauth.datahub.remax.eu/token)

## RESO Posture and Access Gate

Certification is not reachability, and in RE/MAX's case there is not even certification.

- **RESO posture:** RE/MAX is listed as a RESO **Class D Member (Brokers, Agents and Appraisers)** on `https://www.reso.org/membership/`, and RE/MAX holds a seat on the RESO Board of Directors (Joe Wilhelmy, VP of Business Technology, on the 2026 board). RE/MAX does **not** appear anywhere in the RESO certification directory at `https://www.reso.org/certificates/`, which lists 576 certified Data Provider organisations (all of them MLSs, associations and technology vendors). No RESO Web API endorsement, no Data Dictionary endorsement, no UOI, no `$metadata` document, and no Universal Property Identifier reference appears in any RE/MAX-published artifact.
- **Access gate:** `partner-only`. The two documented APIs are RE/MAX Europe's, and their OAuth 2.0 client credentials are issued by RE/MAX Europe to regional master franchisees, offices and their vendors — the Postman documentation ships the literal client_id placeholder `Ask_REU`. There is no signup form, no key-request page and no published pricing. The United States arm publishes nothing at all.
- **Open data:** None. RE/MAX publishes no open, unlicensed, publicly callable dataset. The listing content on remax.com is licensed MLS/IDX data.
- **Auth model:** OAuth 2.0 authorization-code against `https://oauth.datahub.remax.eu/authorize` and `https://oauth.datahub.remax.eu/token`, with the access token then passed as an `access_token` **query parameter** on every request. No OpenID Connect discovery document is served (`/.well-known/openid-configuration` → 404).
- **Home market:** United States (RE/MAX Holdings, Denver, Colorado). The only documented API surface is European.

See [review.yml](review.yml) for the full probe log with HTTP status codes.
