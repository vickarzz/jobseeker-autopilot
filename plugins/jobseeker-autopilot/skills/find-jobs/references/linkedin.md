# LinkedIn rules

LinkedIn's User Agreement prohibits bots and scraping, and accounts can be restricted.
Tell the user this once per session before the first LinkedIn scan.

- Work only in the user's own Chrome, signed in by the user. Never enter passwords.
- Stay sequential: one request at a time, at least 2.5 seconds apart. Never fire parallel fetches (they trigger HTTP 429 and lock the session).
- Cap at about 60 job descriptions per day.
- Search URL: `https://www.linkedin.com/jobs/search/?keywords=<kw>&geoId=<geo>&f_TPR=r604800` (past week; `r86400` = 24h).
- Description text: `fetch('/jobs-guest/jobs/api/jobPosting/<id>')` from a linkedin.com tab, strip HTML.
- Card list: `fetch('/jobs-guest/jobs/api/seeMoreJobPostings/search?keywords=<kw>&geoId=<geo>&f_TPR=<tpr>&start=<n>')`, split on `<li>`, read `jobPosting:<id>`, title, company, location.
- LinkedIn's CSP blocks `eval`; paste full functions each time instead.
- If a page shows an error or rate-limit message, stop LinkedIn work for the session and tell the user.

Common geoIds: Germany 101282230, Netherlands 102890719, Lithuania 101464403, Estonia 102974008,
Saudi Arabia 100459316, UAE 104305776, Qatar 104170880, Singapore 102454443, Indonesia 102478259.
