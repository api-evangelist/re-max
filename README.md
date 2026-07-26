# RE/MAX (re-max)

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
