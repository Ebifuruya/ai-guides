---
layout: default
title: "Prompting Skills Assessment v4.2"
nav_order: 4
---

# Prompting Skills Assessment v4.2

## What This Does

This prompt template asks an AI to review your past conversations and identify specific ways you can get better responses. Instead of giving generic prompting tips, it analyzes how *you* actually prompt — what you already do well and where small changes would make the biggest difference.

The AI will look at your recent chat history, find real examples from your own conversations, and show you exactly how to revise them for better results. Each recommendation includes a reusable sentence or template you can copy and paste into future prompts.

## What You’ll Get

After running this template, the AI will give you a personalized report containing:

- A brief summary of what you already do well (so you don’t lose those habits).
- 3–5 recommended techniques, ranked by how much they’ll improve your results.
- For each technique: a before-and-after example using one of your own past prompts, plus a copy-paste template you can reuse.
- A summary table ranking everything by impact and effort.

## Requirements

- An account with conversation history. The more past conversations available, the better the analysis. At least 10–15 prior conversations are recommended.
- The AI must be able to search your past chats. See the setup instructions below for your platform.

## Setup

### Claude (claude.ai)

1. Open Claude in your browser or app.
2. Go to **Settings** (gear icon, bottom left on desktop).
3. Under **Capabilities**, find **Memory**.
4. Enable **Search and reference past chats**.
5. Return to the main chat screen and start a new conversation.

### ChatGPT (chatgpt.com)

1. Open ChatGPT in your browser or app.
2. Go to **Settings** (your profile icon, then Settings).
3. Under **Personalization**, ensure **Memory** is enabled.
4. Return to the main chat screen and start a new conversation.

**Note for ChatGPT users:** ChatGPT’s ability to reference prior chats may be tied to the Memory setting. If the template doesn’t produce results from your past conversations, verify that Memory is turned on and that you have prior conversation history in your account.

## How to Use

1. Start a **new conversation** (don’t paste this into an existing chat).
2. Copy the entire prompt template below.
3. Paste it as your first message.
4. Send it. The AI will begin searching your chat history and building your report. This may take a minute or two — it has a lot of conversations to review.
5. Read the report and save the reusable templates for future use.

## The Prompt Template

Copy everything inside the box below and paste it as your first message in a new conversation.
```
# Prompt - Prompting Skills Assessment

## Goal

I want to improve the quality of responses I get from LLMs by knowing which prompting changes will make the biggest difference, so I can apply them immediately.

## Role

Prompting skills auditor who evaluates real usage patterns rather than teaching generic best practices.

## Context

### Data Source

My chat history in this account.

## Task

1. Sample broadly across my recent conversations, covering varied task types (research, writing, troubleshooting, comparisons, creative work).
2. Analyze my prompting patterns across the sampled conversations. Identify what I already do well and where gaps exist.
3. For each gap, determine whether the technique was never used or applied inconsistently. Before classifying a technique as inconsistent, evaluate whether the variation across contexts reflects a gap or a deliberate adaptation.
4. Recommend techniques ranked by expected impact on response quality.
5. For each recommended technique:
   a. Explain the technique and why it matters.
   b. Cite a real prompt from my chat history that would have benefited. Show the original, then a revised version applying the technique. Explain what changed and why the revision is better.
   c. Provide a reusable template I can paste into future prompts.
6. Verify each recommendation against my consistent behavioral patterns.
7. When a cited prompt lacks personal context, evaluate whether directives (Audience, Response type, Exclusions, Scope) could achieve the same improvement without adding context. Present directive-based alternatives alongside context-based solutions.

## Format

### Report Structure

1. **Conversation count** — State the number of conversations analyzed.
2. **Strengths summary** — Brief acknowledgment of techniques I already use well. If a technique is already used well, acknowledge it here and move on.
3. **Recommendations** — 3-5 entries ranked by expected impact, each containing:
   - Technique name and explanation
   - Before-and-after example from my chat history with change rationale
   - Reusable copy-paste template
4. **Summary table** — Columns: Technique, Expected Impact (High / Medium / Low), Effort to Adopt (High / Medium / Low). Rank by impact descending.

## Constraints

- Ground every recommendation in patterns observed in my chat history. Do not give generic prompting advice unconnected to how I actually prompt.
- Discard or revise any recommendation that contradicts a consistent behavioral pattern.
- Revised prompts in examples must use only vocabulary and concepts present in or directly inferable from my original prompt.
- Do not recommend adding domain-specific constraints to exploratory prompts.

### Example Selection Rules

Before citing an example in step 5b, verify that I had sufficient domain knowledge at the time to apply the technique:

- The only admissible evidence of prior knowledge is my original prompt and any context provided before it.
- Terms, concepts, or distinctions that first appear in the LLM’s response — not my prompt — are learned vocabulary, regardless of how fluently I employ them later.
- If the technique requires terms I did not have, select a different example.
- If the original prompt contains no domain-specific constraints and follow-up turns show me encountering new terminology for the first time, classify the prompt as exploratory.
```

## Tips for Getting the Most Out of Your Report

- **Run it again in a few weeks.** As your prompting improves, the AI will find different gaps to work on.
- **Try the reusable templates immediately.** Pick one recommendation from your report and apply it to your very next prompt. The techniques are easiest to adopt when you use them right away.
- **Don’t try to change everything at once.** Start with the top-ranked recommendation. Once it feels natural, move to the next one.

## Troubleshooting

**“I don’t have access to your previous conversations”** — The chat history setting is not enabled. Follow the setup instructions above for your platform.

**The AI only analyzed a few conversations** — This can happen if your account is new or if most of your conversations are very short. The more history available, the better the analysis. Come back after you’ve accumulated more conversations.

**The recommendations seem generic** — This usually means the AI couldn’t find enough variety in your chat history to ground its advice. Try using the AI for a wider range of tasks (research, writing, troubleshooting, comparisons) and run the template again later.
