# System Architecture

## Overview
AI-powered recruitment automation workflow built using 
n8n and Google Gemini API.

## Workflow Steps

1. HR submits candidate resume via n8n form trigger
2. PDF text extracted using Extract from File node
3. Resume text sent to Google Gemini with hardcoded JD prompt
4. Gemini returns structured JSON:
   - candidate name and email
   - matched and missing skills
   - experience summary
   - match score out of 100
   - recommendation
5. Results stored in Google Sheets
6. If score >= 70 → shortlist email sent to candidate
7. If score < 70 → rejection email sent to candidate
8. If any node fails → error alert sent to HR

## Tech Stack
- n8n — workflow automation engine
- Google Gemini 1.5 Flash — LLM for resume analysis
- Google Sheets API — candidate result storage
- Gmail API — automated email delivery
- Google OAuth2 — authentication

## Error Handling
- Error Trigger node monitors all workflow nodes
- On failure → HR receives immediate email notification
- Notification includes error message, failed node, timestamp

## Known Limitations
- Runs on localhost — not production deployed
- PDF attachment not available in error emails
- Single job role supported per workflow instance
