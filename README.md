# infiniDome Quote Merger API

Merges monday.com quotes with branded cover and T&C pages.

## Templates
- `infinidome` — infiniDome LTD (Israel)
- `solutions`  — infiniDome Solutions (USA) *(placeholder until PDFs uploaded)*

## Deploy on Render.com
1. Push this repo to GitHub
2. New Web Service on render.com → connect repo
3. Build command: `pip install -r requirements.txt`
4. Start command: `gunicorn app:app --bind 0.0.0.0:$PORT`
5. Add environment variable: `MONDAY_API_TOKEN` = your token

## Zapier Setup
Step 1 — Trigger: monday "Specific Column Value Changed"
  - Board: Quotes & Invoices
  - Column: Status
  
Step 2 — Filter: Status exactly matches "Sent to client"

Step 3 — Webhooks by Zapier: POST
  - URL: https://your-app.onrender.com/merge
  - Payload type: json
  - Data:
    - item_id: [Item ID from Step 1]
    - template: [Quote Generator value from Step 1]
    - upload: true

## Finding your Final Quote column ID
After deploying, call /health to confirm the app is running.
The column ID for "Final Qoute" needs to match what's in monday.
Default assumption is "files9" — update in app.py if different.

## Adding Solutions PDFs
When ready, replace FRONT_SOLUTIONS and BACK_SOLUTIONS base64
strings in app.py with the new PDFs, then redeploy.
