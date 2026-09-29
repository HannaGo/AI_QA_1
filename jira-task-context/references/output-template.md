# `<Task name>`

Source: `<Your instance's Jira URL>/browse/<ISSUEKEY>`
Type: `<Story|Task|Bug>`
Generated: `<YYYY-MM-DD>`

## Goal

`<brief expected outcome of the task>`

## Boundaries

- In scope: `<what's included>`
- Out of scope: `<what's not included, or "Not specified">`

## Requirements

- `<requirement>`
- `<requirement>`
- `<requirement>`

## Additional requirements (from comments)

- `<requirement found in comments that's not among the main requirements>`

## Related Jira context

> This section is for context reference only.
> It is not requirements of the current task and is not
> subject to processing by the next skills.

- `<related_task_ISSUEKEY>`: `<what it gives for understanding the current task>`

## Attachments

- `<description of the attachment per the user's description in chat: type and what it contains>`

---

Section rules:

- Goal, Boundaries, Requirements — always present. If there's no data — "Not specified in Jira".
- Additional requirements (from comments) — only when there are relevant comments with new requirements.
- Related Jira context — only when there are real linked issues in Jira. Comments from the current task are not linked context.
- Attachments — only when there is data.

Formatting rules:

- Metadata (Source, Type, Generated) — each on its own line.
- Each requirement — a separate bullet.
- Don't merge text into one line.
