# Process
By default, projects created in `Azure DevOps` use the `Basic` process. Change this by creating an **inherited** process from `Agile` called `YS Agile` in the `Organization Settings` -> `Boards -> Process`, then assign the project.

![image.png](/.attachments/image-75c6ccc6-09c8-46d7-9999-7d3203d82b64.png)

# Work Item Types and States
The following type and states need to be created in the `YS Agile` process

## User Stories - New Custom Fields
Solution Compliance (new section) with fields:
 - Planned (0 - 100)
 - Actual (0 - 100)
 - Signed-off by (User/Email)

## Enhancements - New Work Item
- Use the `Diamond` Icon in `Pink` color
- Should be based on `Bugs` work item (Should have `Resolved` and `Rejected` state)

## User Stories, Bugs, Enhancements New State
- `Rejected` - `Red Color` (Rejected means re-open)
- `Unresolved` (Unresolved means didn't pass acceptance criteria)


# Work Item Rules
We can enforce certain fields to be required (or any condition) given an event e.g. `State` is changed to `Closed` and etc. We can leverage this to further improve our KPI tracking e.g. for Accuracy Index, Reopen and etc.

![image.png](/.attachments/image-9c182962-5d81-422f-999e-10516a8b18c7.png)

## Enhancements, and Bugs
Make `Completed Work` required whenever change is changed to `Resolved`


# Work Item Fields

## Tasks, Enhancements, Bugs
 - `Original Estimate` should be a required field
 - `Activity` should default to `Development`

## Bugs
Create a new field called `Original Assignee` (Required) that accepts a user for us to track reopen/rejection for bugs more accurately. There are instances that the one who fixes the bug is a different person from the one that caused it.


