# Gmail queries

- `after:<YYYY/MM/DD> (application OR applied OR candidacy OR "your application" OR interview OR assessment OR offer)`
- ATS senders: `from:(greenhouse.io OR lever.co OR ashbyhq.com OR smartrecruiters.com OR myworkday.com OR workablemail.com OR icims.com OR jobylon.com OR teamtailor.com OR oraclecloud.com OR successfactors.com OR linkedin.com)`
- Skip promotions and newsletters.

# Status values

| Status | Signals |
|---|---|
| Submitted | "we received your application", "thank you for applying" |
| In Review | "under review", "shortlisted", "being considered" |
| Assessment | "assessment", "test", "case study", "HackerRank", "Codility" |
| Interview | "interview", "schedule a call", "availability", calendar invite |
| Offer | "offer", "contract", "compensation package" |
| Rejected | "not moving forward", "unfortunately", "other candidates", "position has been filled" |
| Withdrawn | the user withdrew |
| Closed | posting expired before a decision |

Order for "never downgrade": Submitted < In Review < Assessment < Interview < Offer; Rejected / Withdrawn / Closed are final unless a newer email reopens it.
