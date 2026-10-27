---
name: setup-check
description: >
  This skill should be used when the user says "set up jobseeker autopilot", "start jobseeker autopilot", "set up job autopilot",
  "check my setup", "is the plugin working", "health check", "cek setup", "cek plugin",
  or before the first job search in a new account. It verifies that Gmail, Google Drive/Sheets
  and Claude in Chrome are connected and working, and creates the tracker sheet.
metadata:
  version: "0.1.0"
---

# Setup and health check

Run every check below, then report one table: Check | Status (OK / Missing / Error) | What to do.
Never stop at the first failure; finish all checks so the user sees everything at once.

## 1. Connectors

For each connector, load its tools (ToolSearch if deferred) and make one harmless read call.

| Connector | Test call | Needed for |
|---|---|---|
| Gmail | search threads with query `newer_than:1d`, max 1 result | recruiter emails, status sync, drafts |
| Google Drive | search files named "Jobseeker Autopilot" | storing CV and profile |
| Google Sheets | read the tracker (step 2) | tracker |
| Claude in Chrome | `tabs_context_mcp` | filling application forms, LinkedIn |

- Tool absent: status Missing. Tell the user which connector to add in Claude settings (Connectors) or, for Chrome, to install the Claude in Chrome extension and keep Chrome open. If a connector-suggestion tool is available, offer it.
- Tool present but the call errors: status Error, quote the error in one line, suggest reconnecting.
- Chrome present but no browser reachable: status Error, ask the user to open Chrome with the extension signed in.

## 2. Tracker sheet

Search Drive for a spreadsheet named exactly `Jobseeker Autopilot Tracker`.

- Found: read the first row of each tab and confirm these tabs and headers exist; add any missing tab or header.
- Not found: create it with the tabs below, then report its link.

| Tab | Columns |
|---|---|
| Applications | No, Company, Role, Location, Status, Channel, Applied On, Link, Job ID, Match %, Last Update, Notes |
| Profile | Key, Value |
| Filters | Key, Value |
| Skip | Company, Role, Link, Reason, Date |

## 3. Profile and filters

Read the Profile and Filters tabs.
- Empty Profile: tell the user the next step is to share their CV ("upload your CV and say: build my profile").
- Empty Filters: list the filter keys from `${CLAUDE_PLUGIN_ROOT}/skills/fit-check/references/filters.md` and ask for the ones that matter most (countries, minimum salary, visa sponsorship needed, languages, target roles).
- If the user pasted a settings block from the Jobseeker Autopilot web page (it starts with `JOB-AUTOPILOT-SETTINGS`), write each line into Filters / Profile and confirm.

## 4. Summary

End with the table and one line: "Ready" when all checks pass, otherwise the single most important fix.
Do not change any account settings yourself.
