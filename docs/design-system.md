# Design system — product brief

This document defines visual choices for the product. It is not a measured inventory of a running application, CSS export, component recipe or promise of pixel-identical reconstruction. Use the original mockups as inspiration and the product requirements as the behavioral authority.

## Identity

WeEat AI is a warm, food-focused interface with an editorial heading style, restrained leaf/citrus decoration, clear restaurant photography and compact rounded surfaces. Keep food/source context legible. Avoid unrelated dashboard ornament or decorative controls that obscure finding and saving a place.

| Role | Design color |
|---|---|
| Warm canvas | #FAF7F0 |
| Forest brand and major text | #294D3B |
| Deep heading/brand variant | #274E2E |
| Primary orange accent | #FF7224 |
| Readable orange text accent | #C2410C |
| Main ink | #24221F |
| Muted text | #756E65 |
| White surface | #FFFFFF |
| Soft beige surface | #F1EBE0 |
| Neutral border | #E5DED3 |
| Pale green status surface | #EBF4EE |
| Error | #B42318 |

Use orange to identify the main action and selected distance, forest for navigation/selection and cream for the page. Primary-button text/icons must contrast clearly with orange. Provide distinguishable hover, focus, disabled, loading and selected states without relying on color alone. An error does not look like a success notice.

## Type and geometry

Use Playfair Display or a compatible serif for editorial headings, and Inter or a readable sans-serif for interface text. Local font files and licenses are included. Keep headings visually distinct from field labels and compact action text. Allow Vietnamese accents and longer translated labels without clipping.

Use rounded cards, white inputs with visible borders, pill-style buttons/chips and restrained shadows. A compact spacing rhythm should keep related fields together and separate major sections. General design targets are18px card corners,28px hero corners and14px input corners; these are design choices, not exported CSS rules. Interactive targets and focus outlines must remain practical for touch/keyboard use.

Ordinary actions have a consistent comfortable height; compact restaurant actions may use a smaller shared treatment. Match typography, icon size, padding and alignment across equivalent actions rather than inventing a distinct style in every tab. Use a coherent line-icon set; brand/leaf/citrus artwork may be decorative. No React icon modules are supplied.

## Restaurant actions and media

Icons sit to the left of text, centered vertically with consistent spacing. Save is primary in extracted results; Saved stays in the same position. Other variants use the action roles specified in the product brief. Reserve four action positions on supported widths; leave delivery space empty when its action is absent. Keep ShopeeFood unbroken and its external-link icon visible. At very narrow card widths, an orderly second action row is preferable to clipping, squeezing or horizontal page overflow.

Cards have equal outer width within their list regardless of optional actions. Long names/addresses wrap or truncate within that width. Source-preview thumbnails use16:9 and a compact horizontal arrangement of thumbnail, source text and Watch Video; narrow layouts may move the action to another row. Preserve the full source URL through the opening/copying affordance.

Food photographs are not bundled because rights are unverified. Use independently authorized imagery during the build or a neutral fallback. Do not infer that a picture accurately represents an extracted restaurant unless the source data establishes that relationship.

## Responsive requirements

- Mobile is a compact single-column experience. On larger screens Library can become a two-column card grid; Map and chat can use more width, while form-centric screens remain readable rather than stretching edge to edge.
- Use700px as the Library/Map layout transition and600px for chat history/Memory drawer behavior. Test both sides of these transitions. Also inspect small320px and typical390px screens, tablet and desktop.
- Preserve four fixed bottom tabs on desktop as well as mobile. Keep content/composer/dialog actions clear of navigation, safe areas and the on-screen keyboard.
- By Radius and Along Route share white editable-looking FROM fields and filter positioning; adding TO must not disturb unrelated controls. Avoid unnecessary whitespace and jumps.
- Memory is a sidebar on desktop and a closable drawer on mobile. The note list may scroll; Recent Chats should participate in main-page scrolling.
- Text inputs on narrow/coarse-touch devices should be at least16px. Preserve pinch/accessibility zoom. Honor reduced motion, visible focus, sufficient contrast and understandable status/error text.

Original mockups may show obsolete wording, transport controls or claims about services. Do not treat those as required functionality; the product/API specifications govern.
