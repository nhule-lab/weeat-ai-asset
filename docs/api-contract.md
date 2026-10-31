# Target API specification

This specifies product interfaces and data obligations. It supplies no client/server implementation, mock responses, fixture records, module structure or claim that a backend is already connected. Confirm actual service availability, authentication and unresolved fields with the event backend owner before integration.

## Operations

Private operations act on the authenticated user's data. IDs in a request do not authorize access to another user's records.

| Operation | Request | Response | Product obligation |
|---|---|---|---|
| POST /api/analyze | url | video and restaurants | Analyze supported food short; no partial invalid commit; explicit saving required |
| GET /api/library | optional q and cate_id query fields | restaurants | Current-user saved collection and agreed search/category semantics |
| PUT /api/library/{video_id}/{restaurant_id}/save | Target identity in path | is_saved equal to numeric1 | Idempotently save one place |
| DELETE /api/library/{video_id}/{restaurant_id}/save | Target identity in path | is_saved equal to numeric0 | Remove one saved association; preserve shared video/sibling places |
| PATCH /api/library/{video_id}/{restaurant_id} | edits with restaurant_name, dish, price_vnd, address, user_note as supported | restaurant | Return authoritative updated restaurant information |
| POST /api/ask | message and optional session_id | session_id, answer, references | Ground answers and references in the user's saved data |
| GET /api/categories | No business payload | categories | Public category definitions with bilingual labels |
| GET /api/profile | No business payload | profile | Current-user account/profile data |
| PATCH /api/profile | Supported profile fields | profile | Persist explicitly confirmed profile changes |

The response names above are envelope fields, not raw unlabelled arrays. Edit properties belong under the edits request field; profile changes are top-level profile properties. No separate /api/save or /api/config interface is defined here.

## Data vocabulary

| Entity | Contract fields |
|---|---|
| Restaurant | user_id; video_id; restaurant_id; optional doc_id; cate_id; restaurant_name; dish; address; nullable price_vnd and price_vnd_max; nullable latitude/longitude; numeric is_saved; nullable shopeefood_kinds and shopeefood_url; nullable thumbnail_url; optional match_score; user_note; creation/update timestamps where supplied |
| Video | video_id; platform youtube/tiktok; video_url; optional title; nullable thumbnail_url and script_text; analysis duration_seconds and is_food_beverage; optional comments |
| Category | Integer cate_id; cate_name_en; cate_name_vn |
| Profile | user_id; user_email; user_name; user_address; nullable user_lat/user_long; optional age; budget; food_interests; food_notes; timestamps where supplied |
| Budget vocabulary | any, under100,100to250,over250; retain these interface values if the backend supports this optional field, without requiring extra profile controls |
| Reference | video_id and restaurant_id, with optional doc_id/video_url; must resolve to the intended owned restaurant/source |
| Comment | id, text, sentiment good/neutral/negative, likes |
| Confirmed address | Readable formatted label plus latitude/longitude and provider-issued identity where available; manual free text is not confirmation |

Identity combines authenticated user, source video and restaurant. Numeric is_saved accepts0 or1, not an ambiguous truthy string/boolean. One video may contain several restaurants, and a place identifier may repeat across videos. Missing imagery, price, transcript or coordinates must have an honest unavailable presentation.

## Validation and transaction requirements

- A successful extraction has consistent nonempty video/restaurant identifiers, verified current-user ownership, known finite nonnegative duration and an explicit food-and-beverage decision. Each restaurant belongs to the returned source. Reject malformed/foreign-owner responses before persisting data.
- The product scope is short food videos up to approximately five minutes. Settle whether exactly300 seconds is eligible; conflicting prior wording must not become an unstated integration assumption. Unknown duration cannot silently pass validation.
- New discovered identities are unsaved until explicitly saved. Repeated extraction/saving must not create duplicate Library records or erase an existing deliberate save. Failure must not leave a partially saved extraction.
- User edits must not corrupt source attribution. Support minimum-price and note changes as defined above. Maximum-price updates are not defined in the edit interface; either agree an extension during the build or do not offer an action that pretends to save them.
- Profile email is not editable through this form. A home change requires a selected readable address and valid coordinates. Optional API profile fields do not require additional UI controls.
- Delivery is available only for an eligible store result with a valid authorized HTTPS ShopeeFood URL. Search/unknown/unavailable delivery results must not masquerade as store links. Watch uses the source video's URL, never a restaurant/store URL.

## Authentication and failures

Use verified authentication for private requests, with the agreed bearer-token mechanism. Never ship tokens, client secrets or prepared credentials in this package. Configure origins and credentials only during the authorized build. The service must enforce ownership; a visual sign-in gate alone is insufficient.

Use JSON request/response content and an agreed error envelope containing error.code and error.message. Preserve meaningful authentication, validation, permission, not-found, timeout and service-failure distinctions. Provide bounded request behavior and deliberate retry/cancellation where needed. Do not silently fall back from a live service to sample data or label a failed mutation successful.

## Contracts still needed

Autocomplete, reverse geocoding, radius/corridor search, route geometry and agent-managed Memory have no settled HTTP operations in this specification. Agree provider authorization, parameters, response semantics, privacy and error cases during the build. Do not invent endpoints in advance.

Memory integration must support current-user listing, agent-initiated creation, deduplication, confirmed stored deletion and removal from future context. Those are product obligations, not supplied storage code or a pre-existing dummy service. A clearly labeled demonstration may be authored during the authorized session if live integration cannot be completed.
