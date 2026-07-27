---
name: Publish a RE/MAX Europe listing with images
description: Create, image, update and delete a property listing through the RE/MAX Europe Listings API, including how to confirm a queued write actually succeeded through the listing entry logs.
api: collections/re-max-eu-listings-api.postman_collection.json
base_url: https://listing-api-remaxeu.bwscloud.tech/api/v1
environment: staging (the only environment RE/MAX Europe documents)
generated: '2026-07-26'
method: generated
source: collections/re-max-eu-listings-api.postman_collection.json
grounding: >-
  Every request and every field name below appears verbatim in the harvested
  RE/MAX EU Listings API (Staging) Postman collection. RE/MAX publishes no
  OpenAPI, so operations are identified by METHOD + path.
operations:
  - POST /api/v1/listings
  - GET /api/v1/listings
  - GET /api/v1/listings/random
  - GET /api/v1/listings/getByRegionIdAndListingId
  - PUT /api/v1/listings/updateByRegionIdAndListingId
  - DELETE /api/v1/listings/deleteByRegionIdAndListingId
  - POST /api/v1/listings/addImagesByListingIdAndRegionId
  - PUT /api/v1/listings/replaceImageByListingIdAndRegionId/{imageId}
  - PUT /api/v1/listings/updateImageDescriptionByListingIdAndRegionId/{imageId}
  - DELETE /api/v1/listings/deleteImageByListingIdAndRegionId/{imageId}
  - GET /api/v1/listinglogs
  - GET /api/v1/listinglogs/failed
  - GET /api/v1/listinglogs/listingId/{listingId}
  - GET /api/v1/listinglogs/regionId/{regionId}
  - GET /api/v1/listings/countries
  - GET /api/v1/listings/citiesbycountry
  - GET /api/v1/regions/getByRemaxId/{remaxId}
  - GET /api/v1/offices/getByRemaxId/{remaxId}
  - GET /api/v1/agents/getByRemaxId/{remaxId}
---

# Publish a RE/MAX Europe listing

Use this skill to push property listings from a regional system of record into
the RE/MAX Europe Listings API.

## Before you start

- **Only the staging environment is documented.** The published base URL is
  `https://listing-api-remaxeu.bwscloud.tech/api/v1`, on a vendor domain. No
  production base URL is published anywhere - ask RE/MAX Europe for it.
- **Get a token** from `https://oauth.pre-prod.remaxeu-datahub.bwscloud.tech/token`
  and pass it as `?access_token=<token>` on every request.
- **Use the composite-key operations.** Every listing operation exists twice:
  once against an internal surrogate id (`/listings/1`) and once against the
  RE/MAX identity you actually hold (`regionId` + `listingId`). Always use the
  `...ByRegionIdAndListingId` family. `listingId` is unique only within a
  `regionId`.

## 1. Resolve identity first

1. `GET /api/v1/regions/getByRemaxId/{remaxId}` - e.g. `TR1`.
2. `GET /api/v1/offices/getByRemaxId/{remaxId}` - e.g. `AT1-F100199`.
3. `GET /api/v1/agents/getByRemaxId/{remaxId}` - e.g. `ch1-p12345`.

These take RE/MAX Europe Datahub identifiers, which is the seam between this API
and the Datahub API.

## 2. Create the listing

4. `POST /api/v1/listings` with a JSON body. The published field set is
   proprietary - **not RESO Data Dictionary**:

   `listingId`, `status`, `agentUniqueId`, `title`, `description`,
   `roomDescription`, `bathroomDescription`, `bedroomDescription`,
   `kitchenDescription`, `address`, `streetBlock`, `zipcode`, `regionId`,
   `officeId`, `city`, `country`, `offerType`, `listingType`, `buildingSize`,
   `propertySize`, `sizeUnit`, `virtualTour`, `noOfRooms`, `noOfBathrooms`,
   `noOfBedrooms`, `constructionYear`, `energyRating`, `floorNumber`,
   `elevatorAccess`, `outsideAreaType`, `outsideAreaSize`, `listingCurrency`,
   `listingPrice`, `sellPrice`, `dateSold`, `datePublished`,
   `commissionRateBuyer`, `commissionRateSeller`, `contractType`,
   `buyerDemographic`, `sellerDemographic`, `listingUrl`, `listingImages[]`.

   `listingId` is **your** id from your own system, carried through for later
   reference. `listingImages[]` entries are `{ webLink, description }` - images
   are referenced by URL, never uploaded as binary.

5. You can create a listing and its images in a single call by including
   `listingImages[]` in the create body.

## 3. Confirm the write - this step is not optional

**A 2xx on the create does not mean the listing was accepted.** Writes are queued
and validated afterwards. The only way to know the outcome is the entry log:

6. `GET /api/v1/listinglogs/listingId/{listingId}` - the log for your listing.
7. `GET /api/v1/listinglogs/failed` - everything that failed validation.
8. `GET /api/v1/listinglogs/regionId/{regionId}` - region-wide sweep.
9. `GET /api/v1/listinglogs/{id}` - a single log entry.

Poll the per-listing log after each write, and reconcile
`/listinglogs/failed` on a schedule. There is no webhook and no callback.

**There is no idempotency key.** If a create times out, do **not** blind-retry:
call `GET /api/v1/listings/getByRegionIdAndListingId?regionId=..&listingId=..`
first and only retry when the read confirms it is absent.

## 4. Images on an existing listing

- `POST /api/v1/listings/addImagesByListingIdAndRegionId?listingId=..&regionId=..`
- `PUT /api/v1/listings/replaceImageByListingIdAndRegionId/{imageId}?regionId=..&listingId=..`
- `PUT /api/v1/listings/updateImageDescriptionByListingIdAndRegionId/{imageId}?regionId=..&listingId=..`
- `DELETE /api/v1/listings/deleteImageByListingIdAndRegionId/{imageId}?regionId=..&listingId=..`

Note the collection contains a real typo in one documented request -
`regionIdd` on the replace-image call. Send `regionId`; if the call fails,
mirror the documented spelling and report it.

## 5. Update and delete

- `PUT /api/v1/listings/updateByRegionIdAndListingId?regionId=..&listingId=..` -
  send the full body; there is no documented patch semantic.
- `DELETE /api/v1/listings/deleteByRegionIdAndListingId?access_token=..&listingId=..&regionId=..`

Deletes are unguarded and irreversible. Read before you delete.

## 6. Read-side helpers

- `GET /api/v1/listings?page=1&limit=25` - pagination here is `page` + `limit`
  (the Datahub API uses `page` + `size`; they are different APIs).
- `GET /api/v1/listings/countries` and
  `GET /api/v1/listings/citiesbycountry?country=Austria` - geography lookups.
- `GET /api/v1/listings/random` - sampling.

## Errors

The staging origin currently returns an nginx `403` to anonymous callers on every
path, so validate your token before debugging anything else. Application errors
follow the RE/MAX envelope documented in `errors/re-max-error-codes.yml`; queued
validation failures never appear in a response body at all - they appear in the
entry log.
