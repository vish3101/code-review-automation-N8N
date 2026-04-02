# Code Review Automation - n8n

An automated workflow that receives code via email, analyzes it 
using Claude AI, and sends back a structured code review report 
- fully hands-free.

## What It Does

1. Watches Gmail for incoming emails containing code
2. Summarizes the code with purpose, logic, and key components
3. Adds inline comments without changing a single line
4. Drafts a professional HTML email with both the summary 
   and commented code
5. Sends the review back automatically

## Workflow Preview

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d0f55ab6-1bc7-4f0e-b45f-c7ca728a6636" />


## Tech Stack

- n8n (workflow automation)
- Ollama — for all 3 LLM steps
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

## What I Learned

- Chaining multiple LLM calls in sequence in n8n
- Handling HTML rendering issues in Gmail via n8n
- Using Claude API directly via HTTP Request instead of 
  built-in LLM nodes for more control

## Challenges & Possible Improvements

### 1. LLM Speed vs Cost Tradeoff
The workflow was tested with Ollama (local models like Llama3, 
Mistral) which are free but significantly slower — a single 
review can take 2-5 minutes depending on code length. Switching 
to Claude API or GPT-4o brings it down to seconds but adds 
per-request cost. Best approach depends on your volume.

### 2. Prompt Flexibility
Current prompts are opinionated toward a specific output format 
(summary → comments → HTML email). These can be fully customized 
based on what kind of review you need — security audit, 
performance review, documentation generation, or a simpler 
one-paragraph explanation for non-technical readers.

### 3. Single Sender Filtering
Right now the Gmail trigger watches all incoming emails. A cleaner 
setup would use n8n's IF node to filter by specific senders — 
useful if you only want to process code from teammates or clients 
and ignore everything else.

### 4. No Feedback Loop
The system is stateless — it processes and sends but never learns. 
A future improvement could store reviews in Google Sheets and let 
the user rate the output quality. That feedback could then be 
passed back into the prompt as few-shot examples, nudging the 
model toward outputs that actually match what the user wants over 
time.
