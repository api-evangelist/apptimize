---
name: Track an Apptimize event for a user
description: Record a named user event via the Apptimize REST API to drive experiment and feature-flag goals.
api: openapi/apptimize-rest-api-openapi.yml
operations: [trackEvent]
---

# Track an Apptimize event for a user

Record user events that Apptimize uses as goals/metrics for experiments and
feature flags.

## Auth
- Send `ApptimizeApiToken: <API Token>` on the request.
- Use the correct regional host: `https://api.apptimize.com` (NA) or
  `https://api.apptimize.eu` (EU).

## Steps
1. Call `trackEvent` (`POST /v1/users/{user-id}/events/{event-name}`) with the
   user id and the event name in the path.
2. Optionally send a numeric `value` and custom `attributes` (JSON) as
   `application/x-www-form-urlencoded` form fields.
3. A successful call returns `204 No Content`.

## Rules
- The `user-id` must match the identifier used when resolving experiments, so
  events attribute to the right assignment.
- There is no idempotency-key contract; treat event tracking as at-least-once
  and avoid duplicate sends where exact counts matter.
- A `400 Bad Request` indicates a malformed request (e.g. bad attribute types).
