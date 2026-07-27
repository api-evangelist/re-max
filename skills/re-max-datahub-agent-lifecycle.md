---
name: RE/MAX Europe agent lifecycle (person, title, team)
description: Onboard a person into a RE/MAX Europe region, give them a RE/MAX Title at an office, manage their team membership, and terminate them cleanly using the RE/MAX Europe Datahub API.
api: collections/re-max-eu-datahub-api.postman_collection.json
base_url: https://api.datahub.remax.eu/external
generated: '2026-07-26'
method: generated
source: collections/re-max-eu-datahub-api.postman_collection.json
grounding: >-
  Every request below appears verbatim in the harvested RE/MAX Europe Datahub
  Postman collection. RE/MAX publishes no OpenAPI, so operations are identified
  by METHOD + path rather than by operationId.
operations:
  - GET /external/regions/
  - GET /external/offices/
  - GET /external/office/{officeID}
  - POST /external/persons/
  - GET /external/person/{personID}
  - PUT /external/person/{personID}
  - POST /external/person/{personID}/title/
  - GET /external/person/{personID}/history/
  - PUT /external/person/{personID}/changeCurrentPrimaryTitle/
  - GET /external/title/{titleID}/
  - PUT /external/title/{titleID}/transfer/
  - PUT /external/title/{titleID}/exchange/
  - PUT /external/title/{titleID}/end/
  - POST /external/teams
  - POST /external/teams/{teamID}/members
  - GET /external/person/{personID}/memberships
  - POST /external/person/{personID}/terminate/
---

# RE/MAX Europe agent lifecycle

Use this skill to manage the people side of a RE/MAX Europe franchise network:
adding a person, binding them to an office through a **RE/MAX Title**, moving
that title between offices, putting them on a team, and ending the relationship.

## Before you start

- **You need partner credentials.** This API is not self-serve. Ask RE/MAX Europe
  for OAuth 2.0 client credentials; the published documentation carries the
  literal placeholder `Ask_REU` as the client_id.
- **Get a token** from `https://oauth.datahub.remax.eu/token` (authorization code
  flow; the authorize endpoint is `https://oauth.datahub.remax.eu/authorize`).
- **Pass the token as a query parameter**, not a header:
  `?access_token=<token>`. This is how every documented request is shaped. Treat
  it as a logging hazard - do not write full request URLs to logs or analytics.
- **No scopes are published.** Assume the credential is coarse-grained and
  restrict what you do with it yourself.

Failure modes you will hit immediately:

| HTTP | Body | Meaning |
|---|---|---|
| 400 | `{"status":[{"code":4007,"message":"Login parameter Required"}],"result":{}}` | no `access_token` on the request |
| 403 | `{"status":[{"code":4004,"message":"Invalid or expired Session/Token"}],"result":{}}` | token invalid or expired - re-authorize |

There is no RFC 9457 problem+json here; parse `status[0].code`.

## 1. Resolve the region and office

1. `GET /external/regions/` - list the regions your credential can see.
2. `GET /external/offices/?page=1&size=100&sort=uniqueOfficeID` - page through
   offices. Pagination is `page` + `size` + `sort`.
3. `GET /external/office/{officeID}` - confirm the office you are about to
   attach a person to. Office identifiers are region-prefixed, e.g.
   `AT1-F100199`.

## 2. Create the person

4. `POST /external/persons/` - create the natural person record.
5. `GET /external/person/{personID}` - read it back and keep the returned
   `personID` (shape: `FI1-P102962`). **There is no idempotency key on this
   API**, so a retried POST is a probable duplicate person. Read back before
   retrying, and key your own side on the returned `personID`.
6. `PUT /external/person/{personID}` - update address and contact details.

Do not reach for `GET /external/personBySSN/{SSNnumber}` as a convenience lookup.
It resolves a person by national social security number across the network; use
it only where you have a lawful basis, and never log the path.

## 3. Give them a RE/MAX Title

7. `POST /external/person/{personID}/title/` - create the title that binds the
   person to an office. The title, not the person, is the unit of employment.
8. `GET /external/person/{personID}/history/?onlyActive={{onlyActive}}` - list
   current and previous titles.
9. `GET /external/title/{titleID}/` - read a specific title.
10. `PUT /external/person/{personID}/changeCurrentPrimaryTitle/` - when someone
    holds more than one title, set which is primary.

Moving someone:

- `PUT /external/title/{titleID}/transfer/` - move a title to another office.
- `PUT /external/title/{titleID}/exchange/` - exchange a title within the same
  office.
- `PUT /external/title/{titleID}/end/` - end a single title.

## 4. Teams

11. `POST /external/teams` - create a team.
12. `POST /external/teams/{teamID}/members` - add a member.
13. `GET /external/teams/{teamID}/members` - list membership.
14. `POST /external/teams/{teamID}/change-leader` - change the leader.
15. `PUT /external/teams/{teamID}/members/{memberID}` - retire a member.
16. `POST /external/teams/{teamID}/dissolve` - dissolve the team.
17. `GET /external/person/{personID}/memberships` - the person-side view.

Team identifiers are region-prefixed, e.g. `FI1-T100001`.

## 5. Termination

18. `POST /external/person/{personID}/terminate/` - ends **all** active titles
    for that person in one call. This is destructive and has no idempotency
    guard. Confirm with `GET /external/person/{personID}/history/` first, and
    look up the reason vocabulary with
    `GET /external/person/terminationReasons/`.

## Reference vocabularies

All are simple `GET`s that return ID + name pairs, and are worth caching:

`/external/title/types/`, `/external/office/status/`,
`/external/office/specializations/`, `/external/office/conversions/`,
`/external/person/designations/`, `/external/person/languages/`,
`/external/person/genders/`, `/external/person/terminationReasons/`,
`/external/country/states/`, `/external/country/isocodes/`,
`/external/country/phonecodes/`,
`/external/contactInformationEntry/types/`,
`/external/contactInformationEntry/phone/categories/`,
`/external/contactInformationEntry/email/categories/`.

## What this API will not do

No webhooks, no events, no changelog, no rate-limit headers, no deprecation
policy and no status page. Poll, and build your own retry ceiling.
