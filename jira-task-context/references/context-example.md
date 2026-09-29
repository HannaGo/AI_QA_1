# Reference context-file example

This example demonstrates the quality and level of detail
expected from a context file. Use as
a reference for calibration.

> 📌 The example below is entirely made up (project, links,
> people's names, feature). Before using the skill, replace it
> with a real example from your own domain and your
> own project — this significantly improves quality
> calibration for your real tasks.

---

**`DEMO`-1234 - "Save to favorites" button on the list item card and in the details modal**

Source: `<Your instance's Jira URL>/browse/DEMO-1234`
Type: Story
Generated: `<YYYY-MM-DD>`

## Goal
Add a **Save to favorites** button on the list item card and in the item details modal, so the user can quickly add items to a personal collection with corresponding UI states and a limit.

## Boundaries
- In scope: the **Save to favorites** button on the item card and in the details modal, button states (unavailable item — hidden, already favorited — "Favorited"), favorites limit, success message on adding, transition to **View favorites**.
- Out of scope: the "Favorites" page itself and any actions with items inside it — described in a separate epic `DEMO`-1000; this task covers only the add trigger and button states.

## Requirements
- Display the "Save to favorites" button on the item card in the list
- Also display the "Save to favorites" button in the item details modal
- On button click — add the item to favorites
- For unavailable items (archived/hidden) — the button is hidden
- On successful addition — show a success message (text to be clarified later)
- The message can be closed by clicking Close or by clicking outside it
- Favorites limit — 100 items inclusive
- If the limit is reached and the user tries to add more — show an error "Favorites limit reached"
- If the item is already in favorites — show "Favorited" text instead of the button (no action on click)
- If the item is already in favorites — show a "View favorites" button next to it
- Clicking "View favorites" — opens the favorites page

## Additional requirements (from comments)
- Favorites must persist across page reloads (comment by `<comment author name>`, `<YYYY-MM-DD>`: "otherwise the user loses their collection on refresh"; earlier in the discussion it was implied that storage would only persist within the session — the decision was changed to persist across sessions).

## Related Jira context
> This section is for context reference only.
> It is not requirements of the current task and is not
> subject to processing by the next skills.

- `DEMO`-1000: epic "Favorites and personal collections" — the favorites page is described there; the current task is responsible only for the add trigger and button states.

## Attachments
- Success message mockup (PNG, per the user's description in chat) — shows the placement of the Close button and the dimmed background.

---

Why this example is exemplary:
- Goal — one sentence, no filler; Boundaries clearly separates what's included from what's described in another epic (with a reference, not just "out of scope").
- Requirements — atomic bullets, each one action/rule, ready for numbering into REQ-ID by the next skill (requirements-grooming), with no invented details.
- The boundary value is recorded literally ("100 items inclusive"), not generalized ("there is a limit").
- "Additional requirements (from comments)" shows how a comment with a new requirement goes into a separate section (not mixed with the main requirements), and how the "before/after" decision is preserved (session → persist).
- "Related Jira context" shows a linked task that gives background but is explicitly marked as not a requirement of the current ticket.
- "Attachments" records a mockup from the user's description in chat — without inferring details that weren't mentioned there.
