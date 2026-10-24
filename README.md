# AI-Powered Automated LinkedIn Internship Job Tracker

An n8n automation that collects internship listings from an RSS feed, analyzes each posting with Google Gemini, drafts a tailored cover letter, and records the results in Google Sheets.

## What it does

- Runs on a daily schedule.
- Reads job listings from a configured RSS feed.
- Uses Gemini to identify technical skills and draft a role-specific cover letter from the listing details.
- Formats the model response into structured fields.
- Adds a new row to Google Sheets or updates an existing row matched by the job link.

The cover letter is an AI-generated first draft. Review it for accuracy and personalize it before using it in an application.

## Workflow

```text
Daily Schedule
      ↓
Read job listings from RSS
      ↓
Gemini: extract skills and draft cover letter
      ↓
Structured Output Parser
      ↓
Google Sheets: append or update by job link
```

## Built with

- **n8n** for workflow automation
- **Google Gemini** for job analysis and cover-letter drafting
- **RSS Feed Read** node for job listing input
- **Google Sheets** for tracking and deduplicating listings by link

## Data recorded

The workflow is configured to write these fields to Google Sheets:

- Job title
- Job link
- Publication date
- Company/job information
- Job description
- Extracted skills
- Generated cover letter

The current workflow does not define an experience-level output field. Add that to the prompt, structured parser, and sheet mapping if you want to track it.

## Setup

1. Import `workflow.json` into your n8n instance.
2. Configure the RSS Feed Read node with an RSS URL you are authorized to use.
3. Select your own Google Sheet and tab, and confirm its column names match the workflow mapping.
4. Add your Google Gemini and Google Sheets credentials through n8n's credential manager.
5. Check the schedule time and timezone, RSS output fields, structured output, and sheet mapping.
6. Test with a small sample and a test spreadsheet before activating the schedule.

The public workflow file is sanitized: it contains placeholders in place of the original RSS feed and spreadsheet references and does not include saved credential references. Credentials and account connections must be configured in your own n8n instance.

## Implementation notes

The workflow uses a structured output parser to make the model response easier to map into sheet columns. The Google Sheets node is configured to match rows by job link so a repeated listing can update an existing row. Verify these behaviors with test data in your own n8n version before relying on them.

## Privacy and safe use

Job details and generated cover letters are written to the Google Sheet you connect. Use a sheet you control, and do not commit private feed URLs, spreadsheet IDs, credentials, application notes, or unredacted execution data. Treat AI-generated content as a draft and remove unsupported claims before use.

## Project status

This repository contains a sanitized workflow prototype. It has not been verified in another n8n instance. The exported workflow is inactive; configure and test it in your own environment before describing it as production-ready.
