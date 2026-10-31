# RE/MAX

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

RE/MAX Holdings, Inc. (NYSE: RMAX, SIC 6531, Denver, Colorado) is one of the world's largest real estate brokerage franchisors, licensing the RE/MAX brand to independently owned and operated brokerages across more than 110 countries and territories, and franchising mortgage brokerages in the United States under the Motto Mortgage brand with loan processing through wemlo. Its home market is the United States, where it sits in the value chain as a franchisor and consumer portal operator rather than as a data owner: the listing content behind remax.com is licensed from roughly 500 local Multiple Listing Services under IDX and syndication agreements, so RE/MAX is a consumer of MLS data, not a publisher of it. Its API posture reflects that position honestly. RE/MAX is a RESO Class D member (Brokers, Agents and Appraisers) and holds a seat on the RESO Board of Directors, but it does not appear in the RESO certification directory of certified data providers and publishes no RESO Web API, no OData $metadata document and no Universal Property Identifier surface. In the United States there is no developer portal, no published API program and no machine-readable contract of any kind; developer.remax.com, developers.remax.com and docs.remax.com are only wildcard DNS entries pointing at the kvCORE agent website platform, and api.remax.com is a dangling CNAME to a decommissioned booj host that no longer resolves. The only real, publicly documented RE/MAX API surface belongs to RE/MAX Europe, whose Datahub franchise-operations API and Listings API are published as public Postman documentation with OAuth 2.0 authentication, but whose credentials are issued only to RE/MAX regional master franchisees, offices and their vendors — documented, but not self-serve. The only anonymously callable, self-describing RE/MAX endpoint family found anywhere in the estate is the WordPress REST API on the RE/MAX Europe marketing site (remax.eu/wp-json, 42 namespaces and 791 routes), which also exposes an auth-gated Model Context Protocol endpoint via the WordPress MCP Adapter — a CMS surface rather than an API product, but the closest thing to agent-accessible RE/MAX infrastructure that exists today.

**Areas:** Real Estate · United States · Brokerage · Property Listings · MLS · RESO · IDX · PropTech · Franchising · Mortgage · Rentals

## RE/MAX on APIs.io

Everything profiled for RE/MAX is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/re-max/](https://apis.io/providers/re-max/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [RE/MAX Europe Datahub API](https://apis.io/apis/re-max/re-max-eu-datahub-api/) — The RE/MAX Europe Datahub API is the franchise-operations API behind the RE/MAX EU Datahub application. It exposes offices, persons, RE/MAX Titles (the…
- [RE/MAX Europe Listings API](https://apis.io/apis/re-max/re-max-eu-listings-api/) — The RE/MAX Europe Listings API is used in conjunction with the RE/MAX EU Datahub application to add, update, retrieve and delete property listing data and…
- [RE/MAX Europe Site API (WordPress REST)](https://apis.io/apis/re-max/re-max-eu-site-api/) — The RE/MAX Europe marketing site at remax.eu runs WordPress and exposes the WordPress REST API anonymously at /wp-json/. The route descriptor published…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [remax-eu-wordpress-mcp](https://apis.io/servers/re-max/remax-eu-wordpress-mcp/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Re Max Authentication](https://apis.io/security/re-max/re-max-authentication/)
- [Re Max Domain Security](https://apis.io/security/re-max/re-max-domain-security/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.remax.com/)
- [Documentation](https://apidocs.datahub.remax.eu/)
- [Blog](https://news.remax.com/)
- [Privacy policy](https://www.remax.eu/privacy-policy/)

## API Evangelist rating

**Kin Score 18.8** — emerging · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 0.0 |
| Contract governance | 18.2 |
| Operational transparency | 0.0 |
| Developer ergonomics | 47.0 |
| Access clarity | 0.0 |

**Agent readiness 8.5** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | — |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 15.7** — Securities & Market Data

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/re-max/](https://apis.io/providers/re-max/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for RE/MAX: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/re-max/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
