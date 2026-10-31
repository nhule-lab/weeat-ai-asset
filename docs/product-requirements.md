# Product requirements

## Purpose and scope

WeEat AI helps people turn short food videos into identifiable restaurants, save chosen places, explore them by location and ask questions grounded in their saved collection. The relationship must be clear: original video → discovered restaurants → explicit saving to Library.

The product has Discover, Library, Map and Ask AI tabs, with profile completion, restaurant details, sign-in and Memory surfaces. Provide English/Vietnamese interface text without translating users' own messages, restaurant names or addresses. Keep the interface compact and usable on mobile, tablet and desktop.

## Access, identity and profile

- Guests may browse Discover. Analysis and private Library, Map, chat and Memory require authentication. Show clear sign-in guidance and preserve relevant user intent through sign-in.
- An authenticated user can complete a profile without being trapped behind the completion gate. Email is read-only; display name is optional; a confirmed home address is required. Keep the profile form focused; additional demographic/preference fields are not required on this screen.
- A selected home address contains both readable text and valid coordinates. Temporary Map origins must not change the saved profile address.
- Data is isolated by authenticated user. A restaurant is distinguished by user, source video and restaurant identity. Several restaurants can come from one video; the same restaurant identifier in another video must not cause accidental merging.
- If rehearsal needs username/password access, keep it clearly labeled as test access and create credentials during that build. Do not include prepared account data or pretend test access is verified Google authentication.

## Discover and extraction

- Accept supported public YouTube Shorts and TikTok URLs. Reject empty, unsupported or unsafe URLs with understandable correction guidance. Require sign-in before private analysis. Do not invent additional supported platforms.
- Provide Paste Link beside/inside the URL field. Reading clipboard content fills and validates the field; it does not start extraction. Explain denied/unavailable clipboard access and allow manual paste. A delayed clipboard response must not overwrite newer typing.
- Find the food starts one extraction per accepted submission. Prevent duplicate requests. Show inline progress and actionable errors, retaining the ability to retry. Do not save partial or invalid results.
- Enforce a five-minute food-and-beverage scope. Reject non-food content and unknown/invalid duration; settle the exact300-second boundary with the backend before implementation. An empty extraction is different from a successful extraction with places.
- With at least one restaurant, scroll to Just Discovered while keeping its heading visible below fixed controls. Respect reduced-motion preferences.
- Show: “Found your food spots! Save the places you like to keep them in your Library.” Saving is explicit; never auto-save extraction results. Keep individual Save and Save all places, saved-state feedback and success confirmation.
- Below the result heading/description/notice and immediately above Save all places, show a compact source-video preview. Use the supplied thumbnail/title and the original submitted URL. Use a nonmisleading fallback if no thumbnail exists. Do not request metadata solely for this preview.
- Watch Video opens the original source in another tab without repeating extraction. Display the full URL through an accessible opening/copying affordance while truncating its visible presentation as needed.
- Preserve submitted URL, source context, result cards, edits, save states and scroll position when returning from details or other tabs during the active session. Navigation restoration must not rerun extraction. A newly successful source replaces the displayed source/results together. Full-reload restoration is a separate scope decision, not promised here.
- Extracted actions remain Save → Edit → Map → optional ShopeeFood. Saved remains in the first slot. Equal outer card widths and reserved delivery space must not depend on button availability.

## Library and restaurant details

- Library contains only the current user's saved places. Save is idempotent. Removing a saved place requires confirmation and must not destroy another restaurant or its shared source video/transcript.
- Search restaurant name, dish, address, source title and personal note, with accent-insensitive matching. Exclude transcripts from Library search. Do not advertise “search by transcript” or “…or notes…” in the search instruction; removing note wording does not remove note matching.
- Provide platform/category filters, meaningful counts, and recent/oldest/name sorting. Search results, category selection, count and active filters must agree. Distinguish empty Library, no matches, loading and service failure. Let users recover or retry.
- Display name, dish, price or unknown-price guidance, address, thumbnail, source context and available actions. Provide transcript expansion, with an honest unavailable state; no fabricated transcript.
- Let users edit supported restaurant information and saved notes. Cancel preserves stored data; successful edits update every relevant view. Unsupported fields must not pretend to save. Validate required fields, text limits and sensible price ranges in coordination with the API.
- Details preserve the relationship to the original source and offer Edit, conditional Save, Map, source Watch and eligible delivery actions. Return to Discover when opened there, with discovery context intact; otherwise provide Library recovery.
- Comments, when provided, may highlight a small set of favorable/neutral remarks with accessible navigation and pause controls. Exclude negative remarks from this highlight surface; do not invent reviews. Respect reduced motion.

## Map modes

- Use the same compact layout, spacing, typography, white address-input treatment, category filters, result summary and map/result arrangement in both modes.
- By Radius shows FROM only. Along Route shows FROM and TO. FROM looks identical in both modes, with a small Get Current Location action inside the input row. Both distance controls are labeled **Search radius**.
- Default FROM is the user's saved home address. Manual input offers dynamic selectable address suggestions. Only confirmed addresses with valid coordinates can drive radius or route calculations; unselected free text is not a valid location.
- Current location updates FROM only, with a readable reverse-geocoded address. Keep TO, selected distance and category. Permission denial, unavailable GPS and invalid addresses preserve useful state and offer clear recovery.
- Along Route accepts TO from autocomplete, a restaurant card or a map pin. Keep the destination field, selected restaurant, marker, map focus and displayed route synchronized. A manually selected destination remains usable without a restaurant selection.
- Use1,3,5 and10km options, initially5km. Keep a mode's selection stable through address changes. Radius results/circle reflect the confirmed origin; route results reflect the confirmed endpoints and corridor search.
- Expand to5km must select exactly5km, update visualization/results and remove a category restriction if needed to make the expansion meaningful. It must not silently select10km or change the other mode's distance.
- Selecting cards/pins must visibly identify the matching place; Details remains distinct from choosing a route destination. Provide zoom/recenter and useful empty results. Avoid unnecessary layout shifts when switching modes. A separate map-visibility toggle and transport-mode chooser are not required.
- Use genuine provider data only when authorized endpoints exist. A demonstration may be illustrative, but must be labeled and created during the event; never present an illustrative line as a navigable road route.

## Ask AI and Memory

- Answers/recommendations are grounded in the user's saved places, with references that open the correct restaurant/source. Distinguish an empty Library from no matching recommendation. Do not imply unsupported geographic, dietary or allergy guarantees.
- Enter and Send use the same behavior. Clear the draft when accepted for submission, prevent duplicate sends and show the submitted message in the conversation on success. On failure, recover the exact failed draft without overwriting newer input. A late completion must not replace a newly selected conversation.
- Support New Chat, Recent Chats and resuming a selected conversation. Recent Chats scrolls with the main page rather than a nested fixed-height area. Preserve responsive history access and the fixed bottom navigation.
- Keep Memory next to New Chat in the chat actions. It opens **What I remember** as a desktop sidebar and mobile drawer, with close control and scrollable individual rounded note cards, each with a delete icon.
- Memory is read-only except deletion: no Add Memory, input, manual editor or direct creation control. Explicit remember requests in chat create user-associated notes, acknowledge success and update the open panel without refresh. Avoid duplicates/redundancy.
- Confirm deletion before removing the stored note. Successful deletion updates the panel and excludes the note from future AI context; a failure must not falsely hide it. Existing conversation text remains a historical conversation, not an active memory record.
- Empty state: “No memories yet. Ask WeEat AI to remember something in your chat.” Loading and deletion errors are recoverable. “I like hot spicy food” is permitted illustrative copy for a memory interaction, not a supplied stored fixture or automatic reseeding instruction.

## Shared visual and quality requirements

- Reuse the same restaurant action language throughout Discover, Map, Ask AI and Library. Details uses a document/detail icon, Edit a pencil, Map a pin, Watch a play/video icon and ShopeeFood an external-link icon, consistently left of their labels.
- Preserve per-screen action order and primary/secondary roles. Do not add extra actions or rearrange existing ones solely to fill space. ShopeeFood stays on one line, with reserved fourth-slot space when unavailable; allow a slightly wider delivery slot or orderly wrapping of the action grid without widening cards or clipping labels.
- Keep four bottom tabs available at all viewport sizes. Preserve readable input text, safe areas and keyboard clearance. Small/touch text controls should use at least16px to avoid involuntary focus zoom; do not disable user zoom.
- Provide accessible labels, keyboard operation, visible focus, loading/empty/error states, confirmation/cancel behavior and reduced-motion support. No whole-page horizontal overflow.
- Do not silently substitute sample data for failing live services. Keep authentication, extraction, save/edit/delete and conversation privacy intact while integrating the screens.
