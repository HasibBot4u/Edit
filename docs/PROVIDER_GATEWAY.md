# BYOK Provider Gateway and AI Capability Router

**Document ID:** AIVX-API-001 · **Version:** 1.0 · **Status:** PROPOSAL  
**Related:** FEAT-13/14/15, API-031..045, SEC-001..008, TEST-060..069

## 1. Objective

Allow the owner to configure their own AI service credentials and endpoints without tying the app to one model vendor. Credentials are stored and used on the server only. Android sends a provider profile ID and task request, never a secret.

## 2. Provider profile

`ProviderProfile` fields: `profileId`, `ownerId`, `displayName`, `protocolFamily`, `baseUrl`, `endpointOverrides`, `authType`, `secretRef`, `customHeaders` (non-secret values only), `defaultModel`, `requestAdapterId`, `responseAdapterId`, `capabilities`, `limits`, `pricingConfig`, `region`, `timeoutPolicy`, `retryPolicy`, `enabled`, `priority`, `createdAt`, `updatedAt`, `lastTestResult`.

Secret values are separately stored in a secrets vault and represented by `secretRef`. They are encrypted at rest with a managed key service or equivalent. Secret read is prohibited for ordinary database/report endpoints. Secret rotation and deletion are explicit operations.

## 3. Protocol families

- OpenAI-compatible chat/completions or responses (capability-specific; do not assume full API parity).
- Anthropic Messages API style.
- Google Gemini API or OpenAI-compatible endpoint where explicitly supported by vendor.
- Custom HTTP JSON adapter with user-mapped request/response paths, auth header/query field, streaming mode, image/audio/video upload method and error mapping.
- Provider-specific official SDK adapter for features that cannot be expressed by generic JSON mapping.

A service is marked `COMPATIBLE` only after a successful capability test. A base URL alone is not enough.

## 4. Capability manifest

Capabilities are explicit booleans/values: `textInput`, `imageInput`, `videoInput`, `audioInput`, `structuredOutput`, `toolCalling`, `streaming`, `jsonMode`, `longContextTokens`, `maxImages`, `maxVideoDuration`, `maxFileBytes`, `maxOutputTokens`, `supportsTimestamps`, `supportsVideoFrames`, `supportsAudioTranscription`, `supportsBatch`, `supportsTaskPolling`, `region`, `dataRetentionDeclared`, `knownPricing`.

A task router checks capability requirements before it selects the provider. If the profile lacks video input, the orchestrator may extract frames/audio and send those modalities only if the user has allowed that provider to receive them.

## 5. Connection tests

Non-destructive test sequence: validate URL scheme/host; DNS/TLS; confirm no private IP/loopback/link-local/metadata endpoint (SSRF controls); send minimal authenticated text request; optionally test structured output and one small user-authorized media sample; parse response; record latency/error category/model identity/capabilities. The test must not print the secret.

## 6. Security controls

- Do not allow arbitrary user-supplied URL fetching by the Android app backend. Provider endpoints require SSRF protections, domain/IP policy and egress controls.
- Never place secrets in client config, generated Build files, logs, analytics, screenshots, test fixtures or crash diagnostics.
- Redact headers, query strings and provider error bodies before storage/return.
- Limit custom headers and forbid overriding reserved transport/security headers.
- Rate-limit per user/profile; set maximum request/response bytes and timeouts.
- Enforce task-level modality consent and media retention disclosure.
- Store provider task IDs for recovery; do not blindly retry requests that may have billed after timeout.

## 7. Fallback and model routing

Priority is user configuration. Fallback is allowed only when the destination provider has the required modality/capability and the user has permitted that media to be transferred there. No silent cross-provider fallback with private media. Present provider name, destination region and expected cost before first upload to a new provider.

## 8. Tests

TEST-060 secret never appears in Android traffic response or project export. TEST-061 provider key is redacted from logs/errors. TEST-062 mismatched capability blocks task before file upload. TEST-063 unknown custom response schema is marked unsupported, not silently guessed. TEST-064 retry after ambiguous timeout does not duplicate billed task without recovery check. TEST-065 disabled profile cannot be selected. TEST-066 SSRF/private IP target blocked. TEST-067 owner A cannot read owner B provider profile/secret. TEST-068 provider deletion clears vault reference and scheduled metadata. TEST-069 cost limit blocks new jobs and returns clear reason.
