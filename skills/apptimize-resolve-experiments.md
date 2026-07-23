---
name: Resolve Apptimize experiments for a user
description: Fetch a user's variant assignments — code blocks, dynamic variables, feature flags, and full variant info — from the Apptimize REST API.
api: openapi/apptimize-rest-api-openapi.yml
operations: [getVariantInfo, getCodeBlock, getDynamicVariable, getFeatureFlag]
---

# Resolve Apptimize experiments for a user

Use the Apptimize REST API to determine which experiment variants and feature
states apply to a specific user, from any device or backend without an embedded
SDK.

## Auth
- Send the header `ApptimizeApiToken: <API Token>` on every request. The token
  comes from the Apptimize dashboard Install page and is different from the SDK
  App Key.
- Pick the regional host: `https://api.apptimize.com` (North America) or
  `https://api.apptimize.eu` (Europe).

## Steps
1. Call `getVariantInfo` (`GET /v1/users/{user-id}/variant-info`) to retrieve
   all assignments in effect for the user in one call.
2. For a specific code-block variant, call `getCodeBlock`
   (`GET /v1/users/{user-id}/code-blocks/{code-block-variable-name}`).
3. For a typed dynamic variable, call `getDynamicVariable`
   (`GET /v1/users/{user-id}/dynamic-variables/{type}/{dynamic-variable-name}`).
   The `type` segment must match the variable's declared type.
4. For a feature flag, call `getFeatureFlag`
   (`GET /v1/users/{user-id}/feature-flags/{feature-flag-variable-name}`).

## Rules
- Pass targeting context as custom attributes (JSON) in the query string, and
  optionally the `ApptimizeApplicationName`/`ApptimizeApplicationVersion`/
  `ApptimizeOperatingSystem`/`ApptimizeOperatingSystemVersion` headers.
- A `400 Bad Request` means an invalid dynamic-variable type or a wrongly typed
  default — verify the `type` segment matches the variable definition.
- These GETs are read-only and safe to retry.
