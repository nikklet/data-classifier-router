# Incoming Data Classifier and Router

An n8n workflow that reads incoming requests, classifies them with an LLM, and sends each one to the right department.

> **Note:** Built for client work. Code, screenshots, and client details are confidential. This page describes the approach only.

## The Problem
All incoming requests landed in one place, and someone had to read each one and forward it to the right team. That added delay before anyone could act, and items sometimes went to the wrong department.

## How It Works
1. **Receive:** Data arrives through a webhook or API call.
2. **Batch:** Large inputs are split into smaller batches with a Loop Over Items node before processing.
3. **Classify:** An LLM reads the content and returns structured output: department, category, urgency, and a one-line summary.
4. **Route:** A Switch node sends the item to that department's Slack channel or system.
5. **Fallback:** Anything the model can't classify confidently goes to a review queue instead of being guessed.

## Problems Solved
- **Failures on large data volumes.** Large payloads were causing nodes to fail mid-run. I added a Loop Over Items node to split the data into smaller batches, so the workflow processes it in manageable chunks and finishes reliably regardless of size.
- **Inconsistent labels.** The prompt restricts the model to a fixed list of departments, and a structured output parser enforces the format so routing never breaks on unexpected text.
- **Ambiguous requests.** A review fallback keeps uncertain items from being misrouted.
- **Prompt reliability.** I tested the classification prompt against sample requests and refined it until the results were consistent, using the same evaluation approach I use in my AI training work.

## Tools
n8n · Gemini / Claude · OpenAI · Slack API · Webhooks · REST

## Outcome
Reduced handling time by removing the manual sorting step. Requests reach the right team immediately.

## Contact
onwukwetc@gmail.com · [LinkedIn](https://www.linkedin.com/in/tochukwu-onwukwe-9931651b5)
