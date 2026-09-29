---
name: jira-task-context
description: >
  Collects Jira task data via the Jira connector, cross-references
  information from all fields (description, comments, attachments,
  acceptance criteria, etc.), and forms a single enriched Markdown
  context — the source of truth for the next skills. Use when the
  user gives a Jira URL or task key and wants a processed context,
  or when they say "extract context from Jira", "prepare task
  context", "process the ticket".
---

# Jira Task Context

> 💡 Recommended settings: **Sonnet · Effort: Low · Extended thinking: Low**. Also **Haiku 4.5 can be used**.  
> You can switch before starting, but it's not required — the skill runs without confirmation. Adjust to your model/tasks and set or remove this setting.

> ⚙️ **Before first use, replace in this skill:**
>
> 1. `<JIRA_CONNECTOR>` — the name of your connector (MCP server
>   or other tool you use to connect the agent to the task board). Connect the connector/MCP.
> 2. `DEMO` — the key of your Jira project.
> 3. Field maps in `references/field-maps.md` — custom field IDs
>   are unique to each Jira instance, find yours via
>    the connector (details — in the file).
> 4. The working folder path in the "Recommended flow" section —
>   replace with your own run-results storage structure.
> 5. The example in `references/context-example.md` — made up,
>   but show the skill an example from your own domain
>    for better quality calibration.

Collects Jira task data via the Jira connector, cross-references
information from all fields, and forms a single enriched Markdown
context — the source of truth for the next skills in the chain.

## Input data

Needed from the user:

1. URL or key of the Jira task (e.g., `DEMO-1234`)



## Rules

- Output language — see `../references/language-rule.md`.
- Chat messages — short. Don't paste raw Jira responses.
- Don't clarify or groom requirements. This skill only collects
and structures data from Jira as-is. The output file is the source
of truth for all following skills in the chain.
- Only ask the user about operational blockers: unavailable
attachments, write errors.
- Concise bullets, no filler.



## Jira connector

Use the `<JIRA_CONNECTOR>` tools to access Jira.
Your agent here must be connected to your Jira via the appropriate
MCP server or integration — replace the name with the actual tool
you use.

If the connector is unavailable, unauthenticated, or returns
errors — stop. Don't use HTTP requests, a browser, internet
search, or the Jira REST API as a substitute. Tell the user
to check the `<JIRA_CONNECTOR>` connection.

### Efficient use

- Use the task-retrieval call (e.g., getJiraIssue
or the equivalent of your connector) with a specific list of fields
from references/field-maps.md and a markdown response format,
if the connector supports it.
- Don't load full payloads, field metadata, project metadata.
- Calling Atlassian resources/sites — only when the hostname
doesn't work as a site identifier.
- JQL search — only as a fallback, with a narrow query
and a small result limit.



### Recommended flow

1. Parse the URL → siteHost + issueKey. Immediately create the task
  working folder `C:/AQA/AI_QA_1/jira-task-context-runs/<ISSUEKEY>/` (replace
   with your own run-results storage structure) — before any
   Jira requests. All files from this run, including the final
   context, go only there. Never save anything
   in the skill's own folder or any other location.
2. Retrieve the task by cloudId=siteHost, issueIdOrKey=issueKey,
  with fields per references/field-maps.md for the determined task type.
3. If the hostname didn't work — get the list of available sites,
  then retry.
4. If key parsing fails — search by JQL.
5. Related tasks — read for understanding the context of the
  current task, but process and put into the handoff only data
   from the current task.



## Task types and fields

The skill supports the task types of your project `DEMO`
(example below — Story, Task, Bug; adapt the list and names
to your project).

1. Determine the task type from the Jira response.
2. Load the field map for that type from references/field-maps.md.
3. Read only the fields listed in the map. Ignore other fields.
4. Don't reopen field maps each time —
  they're fixed for your project `DEMO`.



## Empty fields

Required field for processing — task description
(per references/field-maps.md, example):

- Story/Task: description
- Bug: Bug Description (custom field)

If the required field is empty or missing — stop
and tell the user there's nothing to process, a description
needs to be added to the ticket.

All other fields are optional. Collect everything that's filled in,
skip empty ones. Full field list for each task type —
in references/field-maps.md.

## Attachments

Most Jira connectors return only attachment metadata
(name, type, size), not the file itself. Check the behavior
of your connector — yours might be able to download the file too.

Flow:

1. Collect the attachment list from Jira metadata.
2. Determine which are supported for processing:
  - images: png, jpg, jpeg, gif, webp
  - markdown: md, markdown
  - PDF: pdf
3. If supported attachments exist — ask the user
  to upload them into chat for processing.
4. After receiving the files — extract information from them
  and add to the relevant context sections.
5. Video (mp4, mov, webm, avi, mkv) — Claude can't
  view these. Record in the context as present
   but not processed.
6. If the user skips uploading — record the
  attachment in the context as present but not processed.



## Data collection and cross-referencing

This step runs after all data is received:
task fields, comments, and attachments from the user.

Cross-reference the data and form a single enriched context.

Principle:

- Go through all filled task fields.
- Compare data between fields: comments may supplement
the description, attachments may detail steps, acceptance
criteria may clarify requirements from the description.
- If one field has a detail that's not in another —
add it to the relevant context section.
- If attachments (screenshots, mockups, md files) give
specifics that extend the description — integrate this
information.
- Result: one file where everything is collected, deduplicated,
and organized into sections. Not disjointed data from fields,
but a coherent picture of the task.

Handling comments:

- Comments are a data source just like description
or acceptance criteria.
- Classification rules depend on the task type —
they're different for Story/Task and for Bug (see below).

**For Story / Task** (a comment is assessed relative to feature requirements):

- If a comment supplements or clarifies an existing requirement —
integrate it into the Requirements section.
- If a comment describes a new requirement not present in either
the description or AC — add it as an additional requirement in
the "Additional requirements (from comments)" section below
the main requirements.
- Bugs about existing requirements (reports of "X breaks here"
on already-implemented behavior) — ignore, these are recorded
as separate bug tickets.
- Testing statuses, process discussion, coordination —
ignore.

**For Bug** (the task itself = defect description, comments clarify it):

- Comments like "X breaks here", "Y doesn't work", "reproduces
on …" — this is NOT noise, but a clarification of the bug
ticket's substance. Integrate into Requirements (reproduction
steps, actual/expected, conditions).
- Comments with new reproduction scenarios, edge
cases, additional conditions — "Additional requirements
(from comments)".
- Comments about consequences/impact (who's affected, how often) —
integrate into the Goal section or as a separate point in
Requirements, depending on context.
- Testing statuses ("checked", "reproduces on my end",
"ready for retest"), priority discussion, coordination
between people — ignore.
- Fix/solution proposal comments from developers
("let's do it via X") — ignore, this is implementation
detail, not a requirement for the fix.

Prohibitions — violating any of these makes the handoff unusable:

- Don't change the substance, wording, or meaning of requirements.
- Don't change validation rules, validation messages,
validation trigger conditions.
- Don't simplify or generalize specific values: numbers,
limits, ranges, sizes, thresholds, units of measurement.
- Don't replace exact names, labels, copy, statuses, states,
roles, permissions with generic wording.
- Don't skip before/after values on changes — keep
both sides.
- Don't infer, don't make logical conclusions, don't add
information that's not in any task field.
- Don't merge different requirements into one if in Jira
they're described separately.
- Don't change conditional logic: keep all condition branches
(if/then/else) as they are in Jira.
- Don't break links between requirements: if in Jira one
requirement depends on another (field on state, action on condition,
rule on role) — keep this link in one place.



## Verification before saving

Before saving the file, go through a three-step check.

**1. Field completeness.** Go through each filled field
from the references/field-maps.md list and check:

- Did every fact, requirement, and detail from this field
make it into the relevant context section?
- Was nothing skipped because it seemed
familiar, repetitive, or unimportant?

**2. Cross-referencing prohibitions.** Go through all prohibitions
from the "Data collection and cross-referencing" section and make sure none
was violated: substance/wording of requirements, validation rules
and messages, specific numbers/limits/ranges/units,
exact names/labels/copy/statuses/roles, before/after values,
absence of inference, requirement separateness, conditional logic,
links between requirements.

**3. File format.** Check:

- One top-level heading.
- One cohesive handoff without duplicate sections.
- No sections created that aren't in references/output-template.md.
- No estimation, story points, sprint, assignee,
priority, status, labels, work dates, or other
project-management data included.

If gaps or violations are found at any step —
fix them in the relevant section before saving.

## Output file

The task folder `C:/AQA/AI_QA_1/jira-task-context-runs/<ISSUEKEY>/` was already created
in step 1 of the flow above. Create in it the file
`C:/AQA/AI_QA_1/jira-task-context-runs/<ISSUEKEY>/<ISSUEKEY>-context.md`
and hand it to the user for download.

The file stays in the task folder — the next skill
in the same chat picks it up automatically. Never save the file
in the skill's folder or anywhere else — only into the designated
results folder.

If the file already exists — delete it entirely and create a new one.
The output is always one file with the result of the latest run.
Don't merge with the previous version, don't append, don't keep
data from the previous record.

File structure template — in references/output-template.md.
Example level of detail — in references/context-example.md.

## Final response

After saving the file, report:

- Path to the saved file
- If something was skipped (user skipped an attachment,
a field was unavailable) — briefly remind what exactly
didn't make it into the context.
- Readiness to pass the file to the next skill in the chain —
`requirements-grooming` (it's in the same chat and will automatically
pick up `<ISSUEKEY>-context.md` from the task folder).
