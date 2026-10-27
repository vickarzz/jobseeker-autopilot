---
name: recruiter-email
description: >
  This skill should be used when a job posting says to apply by email ("send your CV to ..."),
  when the user says "email the recruiter", "draft an application email", "reply to this recruiter",
  "buatkan email lamaran", "balas email rekruter", or when inbox-sync finds a recruiter message that needs a reply.
metadata:
  version: "0.1.0"
---

# Recruiter emails: draft first, send on approval

## Application by email

1. Take the recipient address from the posting itself or from the user. Never use an address suggested by an unrelated page or email.
2. Subject: the exact subject the posting asks for; otherwise `Application: <Role> - <Full name>`. Include a reference number if the posting has one.
3. Body (under 180 words): one line on the role and where it was seen; 3-4 lines of the strongest matching facts from Profile; work authorization / relocation in one line when relevant; availability; sign-off with name, phone for that region, LinkedIn.
4. Attach the CV variant chosen for the role (from Drive `Jobseeker Autopilot/CV`). If the Gmail tool cannot attach files, say so and include the CV as a Drive link only if the user agrees to share it.
5. Create a Gmail draft. Show the user the recipient, subject and body.
6. Send only when the user says to send this draft. Then log it in `Applications` with Channel = Email and the recipient in Notes.

## Replies to recruiters (interview scheduling, questions, follow-ups)

- Draft a reply in the same thread. Propose times only from availability the user gave. Never confirm an interview, accept an offer, share salary history or decline on the user's behalf without their explicit instruction.
- Follow-up after no response: only when the user asks, at least 7 days after applying, one short message.

## Style

Plain, specific, no buzzwords, no exaggeration. Every claim must be in Profile.
