Agora Partner Outreach — Automation Tool
Live demo → augustinjouve-code.github.io/agora-demarchage

Context
L'Agora EDHEC is a student debate association organizing conferences for up to 900 attendees. Every week, the team needs to prospect new financial partners to fund events. As Partnership Officer, I was spending a full afternoon on this task every single week.

Before — The manual process (a full afternoon)
The old workflow had no automation whatsoever:

Open the Google Sheets tracking table and manually scan which companies had already been contacted to avoid duplicates
Copy-paste the entire table into a Claude conversation along with a "master prompt" written from scratch each time
Ask Claude to suggest new target companies — but without memory of previous sessions, relevant companies already contacted would sometimes come up again
Search for contact emails manually using the Skrapp.io Chrome extension — opening each LinkedIn profile one by one, hovering over the contact, copying the email
Paste all 3 emails back into Claude and ask it to write personalized outreach emails
Manually copy each draft into Gmail, add the association's brochure as an attachment, and schedule the send

Every step was disconnected. One mistake (forgetting a contacted company, wrong email) meant starting over. Time cost: a full afternoon every week.

After — The automated workflow (5 minutes)
A single-page web app that handles the entire process in 4 steps:
Step 1 — Setup
Paste your Anthropic API key and Hunter.io API key (stored locally, never in the code). Copy-paste the Google Sheets tracking table → the app automatically reads it and builds an exclusion list of already-contacted companies.
Step 2 — Generate targets
Click "Generate 7 companies". The app calls the Claude API (claude-sonnet) with the exclusion list included in the prompt. Claude returns 7 new partner targets in structured JSON: company name, sector, LinkedIn contact, exact role, email domain, and a personalized justification for the partnership.
Step 3 — Find emails automatically
For each of the 7 contacts, the app calls the Hunter.io API (email-finder endpoint) with the first name, last name, and company domain. Hunter returns the most likely professional email with a confidence score (0–100%). If no email is found, a manual input field appears.
Step 4 — Generate drafts in Gmail
The app generates a complete prompt with all contacts and emails. This prompt is pasted into Claude.ai, which — via the MCP Gmail connector — writes 7 personalized outreach emails and creates them as Gmail drafts instantly. The user only needs to attach the brochure and schedule the send.

Stack
HTML · CSS · JavaScript · Claude API (Anthropic) · Hunter.io API · MCP Gmail · GitHub Pages

Why GitHub Pages?
The initial version ran as a local HTML file. API calls to Hunter.io failed due to CORS restrictions — browsers block cross-origin requests from file:// URLs. Deploying to GitHub Pages (HTTPS) solved this completely.
