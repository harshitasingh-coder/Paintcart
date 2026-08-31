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

## Flags before sending to Claude Code

- **#3 and #5 look like the same request** (promotional/offer posters) — confirm with the client and merge into one item.
- **#4 and #16 are related** — implement #4 (multi-category support) before #16, so the bug fix isn't overwritten by the data model change.
- **#7 (slow load) and #10 (Shade feature)** are bigger than a single line item — #7 needs diagnosis first, #10 needs its own mini-spec.
- Several items need a quick confirmation with the client (marked in Notes) before Claude Code can implement them precisely — best to resolve these first to avoid rework.

## Files in this handoff

- `README.md` — this tracker (quick overview, status, flags)
- `claude-code-change-request-template.md` — full detailed prompt with guardrails, per-change specs, and screenshot placeholders, ready to paste into Claude Code


