# Homework 1: QA Workflow for Release v26.x.x.x

## 1. Jira Ticket Analysis

Identify the target work items for the release:

- **Target Version:** `v26.x.x.x`
- **Issue types:** `Story`, `Improvement`
  - NOT IN: `Support task`
- **Labels:** NOT IN `engineering`
- **Group by:** Epic
- **Exclude:** Defects

> After filtering, export the resulting list as a **CSV file** from Jira.

## 2. Requirements List

From the exported CSV:

- Create a list of requirements.
- Organize requirements by sections, where each **Epic** represents one section.

## 3. Requirements Traceability Matrix (RTM)

Build an RTM that links Jira epics and stories to generated requirements.

### RTM Fields

| Column | Description |
|---|---|
| Jira Epic Id | Epic identifier from Jira |
| Jira Epic Name | Epic title |
| Jira Story Id | Story identifier from Jira |
| Jira Story Name | Story title |
| Requirement Id | Auto/manual generated ID |
| Requirement Name | Short requirement title |
| Requirement Description | Detailed requirement text |

### Fields to Be Filled After Tests Are Created in TestRail

| Column | Description |
|---|---|
| TestRail Test Id | Test identifier in TestRail |
| TestRail Test Title | Test title in TestRail |
| Test Type | `web` or `API` |

## 4. Test Case Creation

Structure test cases to mirror the RTM:

- One **epic/section** maps to one **test section**.
- One **requirement** may have multiple tests.
- Test types: `web`, `API`.

### Test Case Fields

- **Title**
- **Description**
- **References**
  - Epic Jira Id
  - Story Jira Id
- **Steps**
  - Each step contains an expected result, where applicable.

## 5. Review (Critic)

Perform a review/critique of the prepared requirements and test cases before moving them to TestRail.

## 6. Move Test Cases to TestRail

1. Navigate to the target test suite.
2. Create a test section under the test suite for each epic/section.
3. Move the corresponding test cases under the appropriate test sections.

## 7. Map TestRail Test Cases to the RTM

After tests are created in TestRail:

- Insert the **TestRail Test Case Id** in front of the corresponding Jira ticket entry in the RTM.

## 8. Confluence

1. Navigate to the **Test Strategy** Confluence page.
2. Create a new page titled **"Test Plan v 26.x.x.x"**.
3. Post the final RTM on the appropriate Confluence page.
