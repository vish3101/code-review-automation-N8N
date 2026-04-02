# Code Review Automation — n8n

An automated workflow that receives code via email, analyzes it 
using Claude AI, and sends back a structured code review report 
— fully hands-free.

## What It Does

1. Watches Gmail for incoming emails containing code
2. Summarizes the code with purpose, logic, and key components
3. Adds inline comments without changing a single line
4. Drafts a professional HTML email with both the summary 
   and commented code
5. Sends the review back automatically

## Workflow Preview

[paste your canvas screenshot here]

## Tech Stack

- n8n (workflow automation)
- Claude API (Anthropic) — for all 3 LLM steps
- Gmail — trigger + send
- No paid third-party LLM service needed beyond Claude API

## Nodes Used

- Gmail Trigger
- 3x HTTP Request (Claude API calls)
- 1x Code node (HTML sanitizer)
- Gmail Send

## How to Use

1. Import `workflow.json` into your n8n instance
2. Add your Anthropic API key in the HTTP Request headers
3. Connect your Gmail account
4. Send any email with code in the body to your connected Gmail
5. You'll receive a full review within seconds

## Prompts

All 3 prompts used are in the `/prompts` folder — feel free 
to modify them for your use case.

## Screenshots

[workflow canvas]
[sample email output]

## What I Learned

- Chaining multiple LLM calls in sequence in n8n
- Handling HTML rendering issues in Gmail via n8n
- Using Claude API directly via HTTP Request instead of 
  built-in LLM nodes for more control