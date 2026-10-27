# Profile keys

Source: CV = take from the CV; ask = ask the user; calc = compute from CV dates.

| Key | Source | Example |
|---|---|---|
| full_name | CV | Ahmad Zulfikar Rafsanjani |
| email | CV | name@example.com |
| phone_default | ask | +62 8xx xxxx xxxx |
| phone_<region> | ask | phone_middle_east: +966 5xx xxx xxx |
| location_current | CV/ask | Riyadh, Saudi Arabia |
| nationality | ask | Indonesian |
| linkedin_url | CV/ask | verified URL (open it once to confirm it is not a 404) |
| portfolio_urls | CV | GitHub, demo links |
| headline | CV | Senior BI Engineer, Senior Data Analyst |
| years_total | calc | 15 |
| years_<tool> | calc | years_power_bi: 8 |
| skills | CV | comma list |
| certifications | CV | comma list with year |
| education | CV | one line per degree: school, degree, field, years |
| roles | CV | one line per role: title, company, city, start-end |
| languages | CV/ask | English (professional), Indonesian (native) |
| notice_period | ask | Immediately |
| current_salary | ask (optional) | only if the user wants forms to show it |
| salary_floor_<region> | ask | salary_floor_eu: EUR 3,500 / month |
| hourly_rate | ask (optional) | USD 35 |
| work_auth_<country> | ask | work_auth_saudi: transferable iqama |
| needs_sponsorship_outside | ask | yes |
| willing_to_relocate | ask | yes |
| relocation_package_needed | ask | no, visa support is enough |
| cv_default | auto | file name in Drive |
| cv_<label> | ask | cv_power_bi: use for Power BI focused roles |
| facts_confirmed | ask | free text: extra facts the user confirmed (e.g. "PMP in progress") |
