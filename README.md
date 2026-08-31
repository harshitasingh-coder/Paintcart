# Client Change Requests — Tracker

Summary of all change requests received from the client for the existing app.
Use this as a quick reference/checklist; use `claude-code-change-request-template.md`
for the full detailed prompt to hand to Claude Code.

**Legend:** 🐞 Bug fix · ✨ New feature · 🎨 UI/design · ⚡ Performance

| # | Change | Type | Screen | Status | Notes |
|---|--------|------|--------|--------|-------|
| 1 | Warn admin when adding a duplicate product | ✨ | Admin — Add Product | ⬜ Pending | Confirm: which fields = "duplicate"? Soft warning or hard block? |
| 2 | Editable + auto-detect address bar | ✨ | Front-end — Home page | ⬜ Pending | Confirm: auto-fill vs. suggest on detect; where else address is used |
| 3 | Promotional posters (Deal of the Day, Happy Shopping, Discount) | ✨🎨 | Front-end — Home page | ⬜ Pending | Likely same as #5 — merge |
| 4 | One product shown under multiple categories | ✨ | Admin + Front-end — Category | ⬜ Pending | Data model change (many-to-many); relates to #1 and #16 |
| 5 | Posters of offers | ✨🎨 | Front-end — Home page | ⬜ Pending | Likely duplicate of #3 — confirm with client before building separately |
| 6 | Image option for subcategories | ✨ | Admin — Subcategory | ⬜ Pending | Confirm where image is used on front end |
| 7 | App takes too long to load | ⚡ | Whole app | ⬜ Pending | Needs diagnosis first — ask Claude Code to profile before fixing |
| 8 | WhatsApp icon in bottom panel | ✨ | Front-end — Bottom nav | ⬜ Pending | Confirm WhatsApp number + behavior (direct chat vs. pre-filled message) |
| 9 | Zoom in/out on product images | ✨ | Front-end — Product detail | ⬜ Pending | Confirm: main image only, or gallery/thumbnails too |
| 10 | Build "Shade" feature from scratch | ✨ | Admin + Front-end — Product | ⬜ Pending | Bigger feature — needs its own spec, not a one-liner |
| 11 | Mandatory textbox on "Cancel" in admin panel | ✨ | Admin panel | ⬜ Pending | Confirm exactly which "Cancel" screen |
| 12 | User's email not showing in admin panel | 🐞 | Admin — User details | ⬜ Pending | Confirm which screen(s) affected |
| 13 | Notification icon beside cart | ✨ | Front-end — Top bar | ⬜ Pending | Confirm what triggers a notification |
| 14 | Improve post-signup popup design | 🎨 | Front-end — Signup popup | ⬜ Pending | Confirm style reference, if any |
| 15 | Add rating option for users | ✨ | Front-end — Product page | ⬜ Pending | Confirm: rating only or rating + review |
| 16 | Fix product category shown in subcategory | 🐞 | Front-end/Admin — Subcategory | ⬜ Pending | Related to #4 — sequence #4 first |

---

### Change 1: Warn admin on duplicate product entry
Screen/Page: Admin panel — Add Product screen
Current behavior: Admin can add a product (e.g. a paint of a certain shade/name)
that already exists in the catalog with no check — a duplicate gets created silently.
Requested behavior: When the admin tries to add a product that matches an
already-existing product (e.g. same name + shade/variant, or whatever fields
define uniqueness for this catalog), show a warning/indication before the product
is saved, telling the admin this product already exists. Admin should still be
able to confirm and proceed if they intend to add it anyway (unless the client
wants it hard-blocked — confirm this).
Screenshot: [attach image here, labeled "Change 1"]
Notes: Confirm with client which fields determine "duplicate" (exact name match?
name + shade/color? SKU?), and whether this should be a soft warning
(admin can override) or a hard block.

### Change 2: Editable/detectable address bar on home page
Screen/Page: Front-end home page — address bar
Current behavior: The address bar at the top is not clickable/editable. It doesn't
let the user set or change their delivery address in one flow.
Requested behavior:
  a) Address bar should be clickable and editable — user can tap it and manually
     type/edit their address.
  b) It should save the user's address in one go (no separate confusing steps).
  c) There should also be a "detect my location" option (auto-detect via GPS/
     device location) so the user isn't forced to type manually, but manual
     edit should always remain available as an alternative.
Screenshot: [attach image here, labeled "Change 2"]
Notes: Confirm with client: should detected location auto-fill the address bar
(editable after), or just suggest it? Also confirm where the saved address is
used elsewhere in the app (checkout, delivery estimate, etc.) so nothing else
breaks.

### Change 3: Promotional posters/banners on home page
Screen/Page: Front-end home page
Current behavior: No promotional banners/posters are shown on the home page.
Requested behavior: Add a poster/banner section on the home page for
advertisements — e.g. "Deal of the Day", "Happy Shopping", "Discount" style
banners. Likely a carousel/slider of banners near the top of the home page.
Screenshot: [attach image here, labeled "Change 3"]
Notes: Confirm with client: static banners or admin-manageable (i.e. can admin
upload/change these posters from the admin panel later)? How many banners,
static images vs text+image, and whether they should link anywhere when tapped.

### Change 4: One product visible under multiple categories
Screen/Page: Admin panel — product/category assignment; Front-end — category browsing
Current behavior: A product can currently be assigned to only one category.
Requested behavior: A single product should be assignable to 2-3 categories at
once. Example: one product available in "metal finish" and "wood finish" should
be able to show up under both the Metal category and the Wood category — same
product, multiple categories, not a duplicate product entry.
Screenshot: [attach image here, labeled "Change 4"]
Notes: This is a data-model change (product-to-category likely needs to become
many-to-many instead of one-to-one). Confirm with client: does admin manually
tick multiple categories per product, or should variant-based logic (finish =
metal/wood) auto-assign categories? Check how this interacts with Change 1
(duplicate detection) so the same product isn't flagged as duplicate just for
belonging to multiple categories.

### Change 5: Posters of offers
Screen/Page: Front-end home page
Current behavior: No offer-specific posters/banners exist.
Requested behavior: Add posters showing current offers (this may overlap with
Change 3 — confirm with client whether this is the same banner section or a
separate offers-specific area).
Screenshot: [attach image here, labeled "Change 5"]
Notes: Very likely the same feature as Change 3 (Deal of the Day / Happy
Shopping / Discount posters). Confirm with client before treating as separate
work — if it's the same request, merge with Change 3 so Claude Code doesn't
build two overlapping banner systems.

### Change 6: Image option in subcategory
Screen/Page: Admin panel — subcategory creation/edit screen
Current behavior: Subcategories currently have no option to upload/attach an image.
Requested behavior: Add an image upload option for subcategories, similar to
however category images are currently handled.
Screenshot: [attach image here, labeled "Change 6"]
Notes: Confirm with client where this image should then be used on the front
end (subcategory tile/icon, subcategory banner, etc.) so Claude Code knows what
to build, not just where to upload it.

### Change 7: App takes too long to load
Screen/Page: Whole app (confirm if it's app-wide or specific screens — e.g. home
page, product listing)
Current behavior: App load time is slow/noticeably delayed.
Requested behavior: Improve load/performance time.
Screenshot: [attach image here if available, labeled "Change 7" — a screen
recording or the loading screen may help more than a static screenshot]
Notes: This is a performance investigation, not a simple feature change. Before
handing to Claude Code, try to narrow down: is it slow on app open, on a
specific screen, on image-heavy screens, or on all screens? Ask Claude Code to
first profile/diagnose (e.g. check image sizes, API response times, unnecessary
re-renders) and report findings before making changes, rather than guessing at
a fix blindly.

### Change 8: WhatsApp icon in bottom panel
Screen/Page: Front-end — bottom navigation/panel
Current behavior: No WhatsApp icon/contact option currently exists there.
Requested behavior: Add a WhatsApp icon in the bottom panel that lets the user
reach out via WhatsApp (likely opens a chat with the business's WhatsApp number).
Screenshot: [attach image here, labeled "Change 8"]
Notes: Confirm with client the WhatsApp number/business account to link, and
whether it should open the WhatsApp app directly with a pre-filled message or
just open a chat.

### Change 9: Zoom in/out on product images
Screen/Page: Front-end — product detail page (image viewer)
Current behavior: Users cannot zoom into product images.
Requested behavior: Add pinch-to-zoom / zoom in-out functionality on product
images so users can see details closely.
Screenshot: [attach image here, labeled "Change 9"]
Notes: Confirm with client if this should apply only to the main product image,
or also to the image gallery/thumbnails if there are multiple images per product.

### Change 10: Build the "Shade" feature from scratch
Screen/Page: Admin panel (product creation) + Front-end (product display/filter)
Current behavior: No shade feature exists at all.
Requested behavior: Build a full shade feature from the ground up — admin should
be able to define/add shades for a product (e.g. paint shades), and users should
be able to see and select shades on the front end.
Screenshot: [attach image here, labeled "Change 10"]
Notes: This is a bigger feature, not a small tweak — needs its own scoping
session before handing to Claude Code. Confirm with client: is "shade" just a
variant field on a product, or a separate filter/category on the front end too?
Does each shade need its own image, price, or stock? How does it relate to
Change 4 (multi-category) and Change 1 (duplicate warning)? Recommend treating
this as its own mini-spec rather than a one-line change request.

### Change 11: Mandatory textbox on "Cancel" in admin panel
Screen/Page: Admin panel — wherever the "Cancel" action/option exists (specify:
order cancellation? product edit cancellation?)
Current behavior: Clicking "Cancel" performs the action directly with no reason
captured.
Requested behavior: Add a mandatory textbox that must be filled in before the
cancel action can be confirmed (e.g. reason for cancellation).
Screenshot: [attach image here, labeled "Change 11"]
Notes: Confirm with client exactly which "Cancel" option this refers to (there
may be more than one in the admin panel) — screenshot is important here to avoid
Claude Code applying this to the wrong screen.

### Change 12: User's email not showing in admin panel
Screen/Page: Admin panel — user details/list view
Current behavior: The user's email is not displaying in the admin panel where it
should be visible.
Requested behavior: Fix this so the user's registered email shows correctly in
the admin panel.
Screenshot: [attach image here, labeled "Change 12"]
Notes: This is a bug fix, not a new feature — likely a missing field mapping or
API response issue. Confirm exactly which screen(s) in the admin panel are
missing the email (user list, user detail page, or both).

### Change 13: Notification icon next to cart (top bar)
Screen/Page: Front-end — top navigation bar
Current behavior: No notification icon/feature exists near the cart icon.
Requested behavior: Add a notification icon at the top, positioned beside the
cart icon, along with the underlying notification feature (what notifications
show, when they trigger).
Screenshot: [attach image here, labeled "Change 13"]
Notes: Confirm with client what should trigger a notification (order updates,
promotions, price drops, etc.) — icon placement alone is easy, but the feature
behind it needs scoping.

### Change 14: Improve the post-signup popup design
Screen/Page: Front-end — popup shown right after user signs up
Current behavior: The post-signup popup exists but looks plain/unpolished.
Requested behavior: Make this popup visually nicer (better design — spacing,
colors, imagery, etc.) without changing its underlying function.
Screenshot: [attach image here, labeled "Change 14"]
Notes: Purely visual/UI change — confirm with client if there's a
style reference (brand colors, another app's popup, etc.) they want matched.

### Change 15: Add rating option for users
Screen/Page: Front-end — product page (or order history, confirm which)
Current behavior: Users currently have no way to rate a product/order.
Requested behavior: Add a rating option/feature for users.
Screenshot: [attach image here, labeled "Change 15"]
Notes: Confirm with client: rating only, or rating + written review? Should
rating be tied to a completed purchase? Should it show as an average on the
product page? This affects scope significantly.

### Change 16: Fix product category in subcategory view
Screen/Page: Front-end (or admin) — subcategory listing
Current behavior: Products are showing under the wrong category when viewed via
subcategory (category mismatch/bug).
Requested behavior: Fix the category mapping so products display under the
correct category within subcategories.
Screenshot: [attach image here, labeled "Change 16"]
Notes: Bug fix. Confirm with client which specific subcategory(ies) are
affected, and whether this is related to Change 4 (multi-category support) —
if so, sequence Change 4 before this one since fixing it now may get
overwritten by the multi-category rework.

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Claude Code — Targeted Change Request Template
Use this template every time a client sends new change requests for an existing app. Fill in the bracketed sections, attach the screenshots where indicated, and paste the whole thing to Claude Code as your prompt.
1. Context (keep this at the top every time)
You are working on an existing, already-built application. This is NOT a new build.
Project: [App name]
Location/repo: [path or repo name/branch]
Stack: [e.g. React Native + Node/Express + PostgreSQL]
Important guardrails:
●	Do NOT modify, refactor, remove, or "improve" any existing feature, file, or component other than what is explicitly listed below.
●	Do NOT change unrelated styling, naming, folder structure, or logic.
●	Do NOT upgrade packages, rename variables, or reformat code you weren't asked to touch.
●	If a requested change requires touching shared code (e.g. a shared component used elsewhere), STOP and ask me first instead of assuming.
●	If anything below is ambiguous, ask a clarifying question before making changes.
●	After each change, briefly state which file(s) were touched.
2. Client Change Requests
List each requested change as its own numbered item. One item = one specific, scoped change. Attach the matching screenshot right under each item so Claude Code can see exactly what you mean.

Change 1: Warn admin on duplicate product entry
Screen/Page: Admin panel — Add Product screen
Current behavior: Admin can add a product (e.g. a paint of a certain shade/name) that already exists in the catalog with no check — a duplicate gets created silently.
Requested behavior: When the admin tries to add a product that matches an already-existing product (e.g. same name + shade/variant, or whatever fields define uniqueness for this catalog), show a warning/indication before the product is saved, telling the admin this product already exists. Admin should still be able to confirm and proceed if they intend to add it anyway (unless the client wants it hard-blocked — confirm this).
Notes: Confirm with client which fields determine "duplicate" (exact name match? name + shade/color? SKU?), and whether this should be a soft warning (admin can override) or a hard block.

Change 2: Editable / detectable address bar on home page
Screen/Page: Front-end home page — address bar
Current behavior: The address bar at the top is not clickable/editable. It doesn't let the user set or change their delivery address in one flow.
Requested behavior: a) Address bar should be clickable and editable — user can tap it and manually type/edit their address. b) It should save the user's address in one go (no separate confusing steps). c) There should also be a "detect my location" option (auto-detect via GPS/device location) so the user isn't forced to type manually, but manual edit should always remain available as an alternative.
Notes: Confirm with client: should detected location auto-fill the address bar (editable after), or just suggest it? Also confirm where the saved address is used elsewhere in the app (checkout, delivery estimate, etc.) so nothing else breaks.

Change 3: Promotional posters/banners on home page
Screen/Page: Front-end home page
Current behavior: No promotional banners/posters are shown on the home page.
Requested behavior: Add a poster/banner section on the home page for advertisements — e.g. "Deal of the Day", "Happy Shopping", "Discount" style banners. Likely a carousel/slider of banners near the top of the home page.
Notes: Confirm with client: static banners or admin-manageable (i.e. can admin upload/change these posters from the admin panel later)? How many banners, static images vs text+image, and whether they should link anywhere when tapped.
Change 4: One product visible under multiple categories

Screen/Page: Admin panel — product/category assignment; Front-end — category browsing
Current behavior: A product can currently be assigned to only one category.
Requested behavior: A single product should be assignable to 2-3 categories at once. Example: one product available in "metal finish" and "wood finish" should be able to show up under both the Metal category and the Wood category — same product, multiple categories, not a duplicate product entry.
Notes: This is a data-model change (product-to-category likely needs to become many-to-many instead of one-to-one). Confirm with client: does admin manually tick multiple categories per product, or should variant-based logic (finish = metal/wood) auto-assign categories? Check how this interacts with Change 1 (duplicate detection) so the same product isn't flagged as duplicate just for belonging to multiple categories.

Change 5: Posters of offers
Screen/Page: Front-end home page
Current behavior: No offer-specific posters/banners exist.
Requested behavior: Add posters showing current offers (this may overlap with Change 3 — confirm with client whether this is the same banner section or a separate offers-specific area).
Notes: Very likely the same feature as Change 3 (Deal of the Day / Happy Shopping / Discount posters). Confirm with client before treating as separate work — if it's the same request, merge with Change 3 so Claude Code doesn't build two overlapping banner systems.

Change 6: Image option in subcategory
Screen/Page: Admin panel — subcategory creation/edit screen
Current behavior: Subcategories currently have no option to upload/attach an image.
Requested behavior: Add an image upload option for subcategories, similar to however category images are currently handled.
Notes: Confirm with client where this image should then be used on the front end (subcategory tile/icon, subcategory banner, etc.) so Claude Code knows what to build, not just where to upload it.

Change 7: App takes too long to load
Screen/Page: Whole app (confirm if it's app-wide or specific screens — e.g. home page, product listing)
Current behavior: App load time is slow/noticeably delayed.
Requested behavior: Improve load/performance time.
Notes: This is a performance investigation, not a simple feature change. Before handing to Claude Code, try to narrow down: is it slow on app open, on a specific screen, on image-heavy screens, or on all screens? Ask Claude Code to first profile/diagnose (e.g. check image sizes, API response times, unnecessary re-renders) and report findings before making changes, rather than guessing at a fix blindly.

Change 8: WhatsApp icon in bottom panel
Screen/Page: Front-end — bottom navigation/panel
Current behavior: No WhatsApp icon/contact option currently exists there.
Requested behavior: Add a WhatsApp icon in the bottom panel that lets the user reach out via WhatsApp (likely opens a chat with the business's WhatsApp number).
Notes: Confirm with client the WhatsApp number/business account to link, and whether it should open the WhatsApp app directly with a pre-filled message or just open a chat.

Change 9: Zoom in/out on product images
Screen/Page: Front-end — product detail page (image viewer)
Current behavior: Users cannot zoom into product images.
Requested behavior: Add pinch-to-zoom / zoom in-out functionality on product images so users can see details closely.
Notes: Confirm with client if this should apply only to the main product image, or also to the image gallery/thumbnails if there are multiple images per product.

Change 10: Build the "Shade" feature from scratch
Screen/Page: Admin panel (product creation) + Front-end (product display/filter)
Current behavior: No shade feature exists at all.
Requested behavior: Build a full shade feature from the ground up — admin should be able to define/add shades for a product (e.g. paint shades), and users should be able to see and select shades on the front end.
Notes: This is a bigger feature, not a small tweak — needs its own scoping session before handing to Claude Code. Confirm with client: is "shade" just a variant field on a product, or a separate filter/category on the front end too? Does each shade need its own image, price, or stock? How does it relate to Change 4 (multi-category) and Change 1 (duplicate warning)? Recommend treating this as its own mini-spec rather than a one-line change request.

Change 11: Mandatory textbox on "Cancel" in admin panel
Screen/Page: Admin panel — wherever the "Cancel" action/option exists (specify: order cancellation? product edit cancellation?)
Current behavior: Clicking "Cancel" performs the action directly with no reason captured.
Requested behavior: Add a mandatory textbox that must be filled in before the cancel action can be confirmed (e.g. reason for cancellation).
Notes: Confirm with client exactly which "Cancel" option this refers to (there may be more than one in the admin panel) — screenshot is important here to avoid Claude Code applying this to the wrong screen.

Change 12: User's email not showing in admin panel
Screen/Page: Admin panel — user details/list view
Current behavior: The user's email is not displaying in the admin panel where it should be visible.
Requested behavior: Fix this so the user's registered email shows correctly in the admin panel.
Notes: This is a bug fix, not a new feature — likely a missing field mapping or API response issue. Confirm exactly which screen(s) in the admin panel are missing the email (user list, user detail page, or both).

Change 13: Notification icon next to cart (top bar)
Screen/Page: Front-end — top navigation bar
Current behavior: No notification icon/feature exists near the cart icon.
Requested behavior: Add a notification icon at the top, positioned beside the cart icon, along with the underlying notification feature (what notifications show, when they trigger).
Notes: Confirm with client what should trigger a notification (order updates, promotions, price drops, etc.) — icon placement alone is easy, but the feature behind it needs scoping.

Change 14: Improve the post-signup popup design
Screen/Page: Front-end — popup shown right after user signs up
Current behavior: The post-signup popup exists but looks plain/unpolished.
Requested behavior: Make this popup visually nicer (better design — spacing, colors, imagery, etc.) without changing its underlying function.
Notes: Purely visual/UI change — confirm with client if there's a style reference (brand colors, another app's popup, etc.) they want matched.

Change 15: Add rating option for users
Screen/Page: Front-end — product page (or order history, confirm which)
Current behavior: Users currently have no way to rate a product/order.
Requested behavior: Add a rating option/feature for users.
Notes: Confirm with client: rating only, or rating + written review? Should rating be tied to a completed purchase? Should it show as an average on the product page? This affects scope significantly.

Change 16: Fix product category in subcategory view
Screen/Page: Front-end (or admin) — subcategory listing
Current behavior: Products are showing under the wrong category when viewed via subcategory (category mismatch/bug).
Requested behavior: Fix the category mapping so products display under the correct category within subcategories.

Notes: Bug fix. Confirm with client which specific subcategory(ies) are affected, and whether this is related to Change 4 (multi-category support) — if so, sequence Change 4 before this one since fixing it now may get overwritten by the multi-category rework.
3. Scope Confirmation (final line of the prompt)
Only implement the changes listed above (Change 1 through Change 16). Do not touch anything else in the codebase. Once done, summarize exactly what was changed, file by file.
How to use this each time
●	Copy this whole template into a new note/doc for the client update.
●	Fill in Section 1 once per project (context rarely changes).
●	For every change the client asks for, add one numbered block in Section 2, and drop the relevant screenshot right after that block.
●	Paste the finished document as your prompt to Claude Code.
This keeps every request scoped, screenshot-linked, and prevents Claude Code from wandering into unrelated parts of the app.
