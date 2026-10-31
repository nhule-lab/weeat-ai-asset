# User journeys and interaction requirements

These describe user outcomes and acceptance questions. They do not prescribe handlers, state-library structure, stored fixture formats, scoring formulas or code organization.

## First visit → saved collection

The user opens Discover, understands the short-food-video purpose, pastes a supported link and explicitly requests extraction. Guests receive sign-in guidance; incomplete profiles can choose a home address. The user sees progress, then either a recoverable reason for failure or the discovered places tied to the submitted source.

Acceptance: clipboard filling alone starts no extraction; repeated clicks do not duplicate a request; invalid/non-food results are not partly saved. With places found, the result heading becomes visible, the original source preview appears immediately above Save all and the user is told that saving is required. Individual Save/Save all gives persistent saved-state feedback and confirmation.

## Inspect, edit and return

The user opens a discovered restaurant, checks address/price/source/transcript, edits permitted details or returns without saving. Returning to Discover or switching tabs restores the active result context, updated save/edit state and useful scroll position. Reopening the original video does not repeat extraction. A different successful source updates source preview and restaurants together.

Acceptance: optional delivery never changes the outer card width or shifts the first three actions. Unsaved results remain understandable and accessible during navigation. A new extraction is intentional; back navigation is not a trigger.

## Find a saved place

The user opens Library, searches with or without Vietnamese accents, filters platform/category and changes sort order. Search includes personal notes but not source transcript. The user can expand a transcript, view details, edit a saved note, open the source or an eligible store, or confirm removal from Library.

Acceptance: empty collection differs from no matches and service error. Active filters/counts are comprehensible; recovery controls make clear which filters change. Canceling deletion keeps the place. Confirming removal affects only that saved record and preserves siblings/shared source data. A source-only transcript phrase is not advertised as a Library search capability; chat may use richer grounded content.

## Find places around an origin

By Radius starts at the saved profile home. The user can use current location or type and select an address suggestion. Draft text remains editable but does not masquerade as a confirmed location. Selecting a valid origin recenters the radius and updates eligible saved places while keeping the chosen distance/category.

Acceptance: permission denial/unavailable GPS yields useful guidance and does not discard a valid destination/profile. Distance options show the active choice. Expand to5km means exactly5km in the active mode, and circle, summary and places agree. Pin/card associations are visible and accessible. Temporary Map choices do not save a new profile default.

## Choose a route destination

Along Route shows the same FROM treatment plus TO. The user chooses TO by address suggestion or restaurant card/pin. When both endpoints are confirmed, the destination marker, selected place, map focus, route and corridor results synchronize. A new origin must preserve TO and filters; editing unconfirmed text must not create a route from invalid coordinates.

Acceptance: current location changes FROM only. A manually selected destination works without requiring a restaurant card. Switching modes preserves useful origin/filter/distance preferences while avoiding a stale hidden destination. Do not label an illustrative demonstration as actual navigation. Missing provider support is explained, not replaced by silent sample behavior.

## Ask about saved food

The user asks a question or chooses a suggestion. The draft clears when the message is accepted, sending is visibly pending, and successful conversation content appears with relevant saved-place references. A failed send restores the exact draft unless the user has already entered a newer one. New Chat and selecting Recent Chats work while maintaining separate conversations.

Acceptance: Enter and Send agree; double submission is prevented; late results cannot replace another conversation or newer draft. Empty Library and no matching place have distinct replies. Referenced cards open the intended restaurant/source. Recent Chats scrolls naturally with the page; fixed composer/navigation does not hide messages.

## Ask the agent to remember, then delete

The user explicitly asks the agent to remember a preference. The agent acknowledges successful storage and the Memory panel updates without refresh. For example, the user may ask to remember “I like hot spicy food.” That phrase is illustrative product copy, not a supplied pre-existing record.

The user opens What I remember, reads notes and chooses trash on one note. Cancel keeps it; confirmation removes the stored note and excludes it from future memory context. The user can close the sidebar/drawer and return to chat. Empty/loading/failure states remain useful.

Acceptance: no manual Add/edit/input exists in Memory. Notes belong to the current user. Repeated equivalent requests do not create redundant cards. A deletion error does not falsely hide a note; reopening does not recreate a deliberately deleted note. Old conversation text may still contain a past statement without making it active memory again.

## Profile and repeated usage

The user reviews read-only account email, optionally changes display name, selects a confirmed home address and explicitly saves. Cancel leaves the saved profile intact. On return, Library and conversation data are user-specific; sign-out cannot expose them to another user.

Acceptance: profile completion is reachable before other gated features; free-text address alone cannot complete it; Map GPS/manual use never silently updates it. Errors preserve recoverable drafts. Keyboard, touch, translation, reduced motion and narrow layouts remain usable throughout these journeys.
