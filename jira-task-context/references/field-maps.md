# DEMO Jira Field Maps

> 📌 **Fill in this file yourself, before first using the skill.**
> All fields in the tables below — both the row names ("User story",
> "Notes for DEV", "Bug Description", "Affected by", "Impact
> Analysis", etc.) and their keys/IDs — are just an example from
> the original skill. In your project, custom fields are almost
> certainly named and arranged differently: different names, different
> count, different IDs (`customfield_XXXXX` are unique to each
> Jira instance). Treat each table row as a demonstration
> of the "Value | Field key | Required" format, not as a ready-made
> list of fields. To build your own:
> 1. Via your Jira connector, call field metadata for the task type
>    (e.g., getJiraIssueTypeMetaWithFields or an equivalent) —
>    it will return the list of fields, their names, and IDs for the
>    specific project and task type.
> 2. Or open a task in Jira → "..." → "Configure fields" /
>    project field administration, if you have access.
> 3. Rebuild the tables below: remove fields not in your
>    project, add the ones that are there, enter the real IDs and names.
>
> Standard fields (`summary`, `description`, `comment`, `attachment`)
> are usually the same across any Jira instance and can be left as is,
> but still cross-check against a real task — some projects rename
> even these at the display level.

Fixed field maps for project `DEMO`. Don't reopen
these maps each time — use as is, after one-time
setup.

For all types: exclude service/counter fields that carry no
meaningful information (example from the original: a comment-count
counter field). Find the equivalents in your project and exclude them here,
if any.

All fields in the examples below are examples and custom fields.
Update the fields from your own Jira tickets.

## Story

| Value | Field key | Required |
|---|---|---|
| Name | summary | — |
| Description | description | yes |
| User story | `<User_story_field_ID>` | no |
| Acceptance criteria | `<Acceptance_criteria_field_ID>` | no |
| Notes for DEV | `<Notes_for_DEV_field_ID>` | no |
| Notes for QA | `<Notes_for_QA_field_ID>` | no |
| Affected by | `<Affected_by_field_ID>` | no |
| Comments | comment | no |
| Attachments | attachment | no |

## Task

| Value | Field key | Required |
|---|---|---|
| Name | summary | — |
| Description | description | yes |
| Acceptance criteria | `<Acceptance_criteria_field_ID>` | no |
| Notes for DEV | `<Notes_for_DEV_field_ID>` | no |
| Notes for QA | `<Notes_for_QA_field_ID>` | no |
| Affected by | `<Affected_by_field_ID>` | no |
| Comments | comment | no |
| Attachments | attachment | no |

## Bug

| Value | Field key | Required |
|---|---|---|
| Name | summary | — |
| Bug Description | `<Bug_Description_field_ID>` | yes |
| Notes for QA | `<Notes_for_QA_field_ID>` | no |
| Notes for DEV | `<Notes_for_DEV_field_ID>` | no |
| Affected by | `<Affected_by_field_ID>` | no |
| Impact Analysis | `<Impact_Analysis_field_ID>` | no |
| Attachments | attachment | no |
| Comments | comment | no |
