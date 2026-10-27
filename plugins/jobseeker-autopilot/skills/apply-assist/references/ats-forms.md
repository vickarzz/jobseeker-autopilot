# Form patterns by ATS

## LinkedIn Easy Apply
- Contact page: set phone country code and number to the regional phone.
- Resume page: pick the CV; check the prefilled cover letter and replace it (it may be from another job).
- Radio questions are DIVs: click by coordinates from a screenshot; `form_input` fails on them.
- Last page often has a consent checkbox: leave it.

## Ashby (jobs.ashbyhq.com)
- Upload the CV first; it autofills name and email. Wait ~10 s for parsing.
- Location is a combobox: type the city, pick from the list.

## Greenhouse / Lever / SmartRecruiters / Workable
- Standard inputs; `form_input` works. Location fields are often autocompletes.
- SmartRecruiters often ends with a diversity survey: leave it.

## Workday (*.myworkdayjobs.com)
- Needs an account: the user signs in.
- Text fields: `form_input`. Date spinbuttons: click, then type MMYYYY.
- School / field / skills: type, press Enter, pick the option checkbox. If the skills input ignores JS, focus it and type with the keyboard.
- "VPS" or save errors are server-side: ask the user to sign in again.

## Oracle Recruiting (fa.ocs.oraclecloud.*)
- Starts with email + terms checkbox (user ticks). Phone country code is a combobox: type the country name, pick "+NN (Country)".
- Sessions expire quickly; refill if redirected to the job page.

## iCIMS (*.icims.com)
- The form lives in a same-origin iframe. Fill via `iframe.contentDocument` with native value setters + change events.
- File upload inside the iframe cannot be automated: ask the user to click "My Computer".
- Country is a searchable dropdown: click, type, pick.

## Teamtailor / Jobylon / Personio / Cornerstone (csod)
- Standard forms. Jobylon phone uses a flag picker with a search box: open it, type the country, pick, then type the number.
- Cornerstone checkboxes may need a real click after `form_input`.
