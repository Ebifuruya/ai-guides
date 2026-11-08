---
layout: default
title: "Prompt Directives Guide v8.3"
nav_order: 3
---

# Prompt Directives Guide v8.3

A practical guide for writing better LLM prompts. No programming knowledge is required.

---

## Why Directives Exist

When you type a question into an AI assistant without additional instructions, the AI must guess everything else: who you are, what you already know, what kind of answer you want, and what to include or leave out. These guesses are often wrong.

For example, if you ask *"What are the best anti-aging supplements?"* — the AI will guess you want a general overview for a beginner, with safety disclaimers. If you actually want a comparison of clinical evidence for specific compounds, the response wastes your time.

Directives fix this. Each directive replaces one guess with an explicit instruction.

---

## What Are Directives?

A directive is a labeled instruction at the beginning of your prompt. It has two parts: a **label** (such as "Goal" or "Audience") and a **value** (the instruction itself). Together, they tell the AI one specific thing about how to handle your request.

Here is a simple directive:

```
## Audience
People who have never built a computer before.
```

This single line changes the entire response. Without it, the AI might skip basic explanations. With it, the AI adjusts its vocabulary and adds more detail.

Most prompts need only two to four directives — the ones that correct the AI's most likely wrong guesses.

| Directive | Definition | Example |
|---|---|---|
| Goal | *What am I trying to accomplish?* The decision, choice, or action this output will support — the AI optimizes its response around this | I need to decide which laptop to buy by Friday |
| Role | *Who should the AI be?* A professional identity the AI adopts — determines expertise and perspective | skincare science educator |
| Context | *What does the AI need to know?* Background information and supplied data the AI cannot infer — facts, attachments, data sets, links, quoted material, and domain knowledge | I have sensitive skin that reacts to fragrance |
| Task | *What should the AI do?* The work the AI performs — the action and what it acts on | compare these three serums on price, ingredients, and ratings |
| Audience | *Who will read this?* The reader's knowledge level and perspective | adults over 50, new to skincare routines |
| Tone | *How should it sound?* The voice, register, and warmth of the response | friendly and practical, not academic |
| Format | *What should it look like?* The output's type, structure, and dimensions | comparison table, then one-paragraph summary |
| Constraints | *What rules govern the output?* Restrictions, requirements, and limits on what the response contains or excludes | budget under $30; omit disclaimers and beginner definitions |

Each directive in the table above owns an exclusive scope — a distinct aspect of the prompt that no other directive governs. Task controls the work the AI performs. Constraints controls what the response contains. Format controls the response's shape. And so on. A well-written prompt instruction fits cleanly inside one directive. When a single instruction spans two scopes — telling the AI what to *do* and what to *include* in the same sentence — split it into two instructions and place each under the directive that owns that scope.

### Splitting Blended Instructions

The most common scoping mistake is a blended instruction — a single sentence that contains work belonging to two different directives. This happens most often at the Task–Constraints boundary, where a process step and an output rule are written as one thought.

**Example — a blended instruction:**

> Verify each claim against published sources and report the verification status in the output.

"Verify each claim" is a process step — it belongs in Task. "Report the verification status" is an output rule — it belongs in Constraints. Written as one instruction, it is ambiguous about which directive controls the behavior.

**After splitting:**

```
## Task
Verify each claim in the attached article against published sources.

## Constraints
Include the verification status (confirmed, unconfirmed, or refuted) for each claim.
```

Task now tells the AI what to do. Constraints tells the AI what to include. Each directive reinforces the other without ambiguity about ownership.

**How to spot a blend:** If a single instruction contains both an action the AI performs *and* a rule about what the response should contain, it spans two scopes. Rewrite it as two instructions — one for each directive.

### Boundary Reference

When an instruction belongs to one directive but you are unsure which one, use these resolutions.

**Goal ↔ Context.** Goal is what the user wants to happen next. Context is what has already happened or is currently true.

**Goal ↔ Task.** Goal is the user's intended outcome. Task is the AI's action toward that outcome.

**Task ↔ Format.** Task is the work the AI performs. Format is the shape of what it produces.

**Task ↔ Constraints.** Task controls process — what the AI does and considers. Constraints controls the response — what it contains or excludes.

**Context ↔ Constraints.** Context is information the AI should factor in. Constraints are rules the AI must obey.

---

## Where Instructions Belong

When you are unsure which directive an instruction belongs in, use this table. Each row shows an instruction and the directive it maps to.

| Instruction | Directive |
|---|---|
| I need to choose a contractor by Friday | Goal |
| I want to understand which supplement has the strongest evidence | Goal |
| Financial advisor | Role |
| Senior editor at a medical journal | Role |
| The company switched CRM vendors last quarter | Context |
| I have a 1920s bungalow with plaster walls | Context |
| This study used a sample size of 200 patients | Context |
| Compare these three options and recommend one | Task |
| Summarize this report | Task |
| Homeowners with no construction background | Audience |
| Graduate students in molecular biology | Audience |
| Direct and concise | Tone |
| Warm and encouraging, not clinical | Tone |
| Numbered list with one paragraph per item | Format |
| Under 200 words | Format |
| Side-by-side comparison table | Format |
| Omit disclaimers and generic advice | Constraints |
| Budget: $500 | Constraints |
| Do not recommend products that require a prescription | Constraints |
| Verify each claim and report verification status | ⚠ Split — see above |
| Summarize the report and keep it under 200 words | ⚠ Split — see above |

---

## Prompt Structure

Prompts use **Markdown heading levels** to organize directives. This structure works in Claude, ChatGPT, and Gemini.

**Tip:** For prompts longer than a few directives, draft in a Markdown editor (such as Typora, MarkText, or VS Code) rather than directly in the chat window. Most chat interfaces submit the prompt when you press Enter, which can send an incomplete draft. Compose in the editor, then paste the finished prompt into the chat.

**Rules:**

- `##` is reserved for directives. Every directive is a `##` heading, and every `##` heading is a directive. Nothing else uses `##`.
- `###` is reserved for operands — sub-sections that belong to the directive above them. A `###` heading is always an operand of the nearest `##` above it.
- `#` (single hash) is reserved for the prompt's title. It appears once, on the first line. Titling your prompts is recommended — it makes searching through past chats and reviewing saved templates significantly easier, because the AI's auto-generated chat titles are often vague or uninformative. Prompt templates should always include it. No other content uses `#`.
- All directives sit at `##` (equal importance). Operands sit at `###` (subordinate to the directive above). Deeper nesting is permitted: a `####` nested section may sit inside a `###` operand. Each heading level nests inside the level directly above it — do not skip levels (e.g., `####` directly under `##` without an intervening `###`).
- Content between a `##` or `###` heading and the next heading of any level belongs to the section above it.

**Example:**

```markdown
## Context
### Tools
- Notion
- Asana
- Monday.com

## Task
Compare these project management tools for a small design team.

## Audience
Non-technical team leads choosing their first project management tool.

## Format
Comparison table, then a one-paragraph recommendation.
```

"Tools" uses `###` instead of `##`, placing it under Context as a data operand — the static list the Task acts on.

Place directives before the question or request so the AI reads the instructions before encountering the task.

---

## Nesting: Directives and Operands

Some directives need more than a sentence — a Task might describe a multi-step approach, or a Format might include a detailed output template. This additional content is called an **operand** — a `###` sub-section that extends the directive above it. Operands come in three types:

**Data operands** hold static, non-instructive content: lists, tables, quoted text, file-attachment descriptions, pasted data, or links to external material. Data operands belong exclusively under **Context**. Placing data under any other directive misrepresents it as an instruction.

**Instructive operands** hold specifications, templates, steps, or structured instructions that extend a directive's behavior. Instructive operands belong under the directive they serve — a step-by-step approach under Task, an output template under Format, grouped restrictions under Constraints.

**Organizational operands** separate and label blocks of text that need their own section — definitions, explanations, clarifications, issues, or non-binding recommendations. Use an organizational operand when bullet lists, block quotes, or other inline formatting cannot adequately separate the content. Organizational operands appear most often under Context but may appear under any directive.

The heading hierarchy enforces ownership:

- A `###` operand is owned by the `##` directive above it — always.
- Content placed after a `###` heading belongs to that operand until the next heading of any level.
- If an operand is placed under the wrong directive, the AI associates it with whatever directive it falls under structurally, not with the directive the author intended.

**Example** — data operand under Context, instructive operand under Format:

```markdown
## Context
### Shoes
- Nike Vaporfly 3
- Asics Gel-Nimbus 26
- Brooks Ghost 16

## Task
Evaluate the shoes for marathon training.

## Format
Side-by-side comparison.

### Output Structure
One section per shoe covering cushioning, weight, durability, and price.
Final paragraph with a pick for different runner types.
```

"Shoes" is a data operand — a static list the Task acts on — so it sits under Context. "Output Structure" is an instructive operand — a template that specifies how Format should behave — so it sits under Format.

### Naming Operands

Name each `###` sub-section for what it contains, not from a fixed vocabulary. A list of contractors becomes `### Contractor Bids`. A desired output template becomes `### Output Structure`. A set of error messages to diagnose becomes `### Error Log`. The label should tell the AI (and a future reader) exactly what the sub-section holds.

### When to Use an Operand

Add a `###` operand when a directive contains structured content — a data list, a template, a multi-line specification, or a block of text that needs its own labeled section — that would clutter the directive's main instruction. If the content fits naturally in one or two sentences, keep it in the directive's body.

### Which Directives Use Operands

- **Context** — data operands: lists, tables, attachment descriptions, quoted or pasted data, links to external material. Organizational operands: definitions, issues, explanations, clarifications, non-binding recommendations or proposed solutions. Name each operand for its content (e.g., `### Contractor Bids`, `### Attachments`, `### Definitions`, `### Issues`).
- **Task** — instructive operands: when the approach requires specification (e.g., `### Steps`, `### Method`).
- **Format** — instructive operands: when the output structure needs a template (e.g., `### Output Structure`) or a sample demonstrates the desired style (e.g., `### Example`).
- **Constraints** — instructive operands: when restrictions span several categories and benefit from grouping.

Organizational operands may also appear under other directives when content needs structural separation, though this is less common than under Context. Most directives beyond Context are a sentence or two and need no operands.

### Nested Sections

A **nested section** is any heading at `####` or deeper that sits inside an operand. Nested sections subdivide an operand's content when it is too long or complex for a single block.

```markdown
## Context
### Issues
#### Formatting inconsistencies
The report mixes metric and imperial units throughout.

#### Missing citations
Sections 3 and 7 reference studies without bibliographic entries.
```

"Issues" is an organizational operand under Context. "Formatting inconsistencies" and "Missing citations" are nested sections inside that operand.

**Rules:**

- Every nested section must sit inside an operand — never directly under a directive.
- Do not skip heading levels: `####` nests inside `###`, `#####` nests inside `####`.
- All three operand types — data, instructive, and organizational — may contain nested sections.

### How the AI Treats Context Content

The AI reads Context as information, not as instructions. Facts, data, and background in Context inform the AI's thinking, but any instructions embedded there — a style guide, a checklist, a set of corrections — remain inert by default. The AI will not follow them unless another directive explicitly references them.

**Activating Context instructions.** A reference from an instructive directive — Task, Constraints, or Format — gives the referenced Context content instructive power. For example, if Context contains an attached style guide, adding "Follow the style guide in the Context" to Constraints activates it.

**Bundled activation.** When Context describes several issues or includes multiple instructions, you do not need a separate reference for each one. A single Task instruction — such as "Address all issues described in the Context" — activates every embedded instruction at once. This keeps Task lean and avoids excessive back-and-forth between directives.

**Priority.** Activated Context instructions are subordinate to the directive that activated them. If a Context instruction conflicts with an instruction in its activating directive, the activating directive wins.

---

## Formatting Tools

Several Markdown tools help organize content within directives.

| Tool | Syntax | Use For |
|---|---|---|
| Bullet list | `- item` | Unordered items |
| Numbered list | `1. item` | Ordered steps, rankings |
| Code block | ```` ``` ```` | Data the AI should not interpret as instructions |
| Block quote | `> text` | Quoted passages |
| Inline literal | `` `text` `` | Exact terms, file names, error messages |
| Link | `[Label](URL)` | Clickable references |
| Escape | `\#` `\*` | Literal special characters |

**Platform note:** Claude and Grok close code blocks automatically. ChatGPT requires closing backticks. When pasting from an external editor, include both opening and closing backticks.

---

## When to Use Each Directive

| Directive | Include When | Omit When |
|---|---|---|
| Goal | Same task could serve different purposes | Purpose is obvious from the task |
| Role | Specific expertise changes the answer | Task + Audience suffice |
| Context | Answer depends on information the AI cannot infer | Question is general-purpose |
| Task | Question could produce different output types | Question is unambiguous on its own |
| Audience | Reader knowledge ≠ AI's default assumption | Defaults work |
| Tone | Default voice wrong for audience or purpose | Defaults work; or Role implies it |
| Format | Specific output type, structure, or dimensions needed | Default format acceptable |
| Constraints | Any restrictions on what appears in the output | No restrictions needed |

### Additional Guidance

**Goal** — Goal states what you need the output for, not what you want the AI to do (that is Task). The same task — "summarize this paper" — produces different responses depending on whether the goal is to decide if the paper is worth reading, to include it in a literature review, or to brief a non-technical manager. The AI uses the goal to optimize its entire response: it will not suggest a three-day process when the goal says "by tomorrow." When the goal is obvious from the task, omit it.

**Role** — Keep Role to a professional identity. If you find yourself adding clauses about what the role does — *"financial advisor who evaluates contractors objectively"* — those clauses belong in Task. "Financial advisor" sets the perspective (Role's scope); "evaluates contractors objectively" describes work the AI performs (Task's scope). Split them. A well-defined Task and Audience often make Role unnecessary.

**Context** — Context supplies background the AI cannot infer and all supplied data: facts about the user or domain, file-attachment descriptions, data sets, quoted material, and links. Use data operands (`###` sub-sections) to organize supplied data by content (e.g., `### Attachments`, `### Survey Results`). The AI reads Context as information by default — any instructions embedded in supplied data remain inert unless another directive references them. When you want an unbiased, general-purpose answer, Context can unintentionally narrow the response — use Audience and Format instead.

**Task** — Task is the AI's process — what it does, analyzes, or reasons through. When the task acts on supplied data (product lists, URLs, documents), place that data in Context as a data operand and reference it from Task. Instructions about what the response should contain or exclude belong in Constraints, not Task, even when they feel like part of the same thought.

**Format** — Format encompasses both the output type (evidence review, buying guide, troubleshooting checklist) and its structure (table, numbered steps, word count). Name the type first, then describe the structure. Specifying a type like "evidence review" can shift the AI from its default advice mode to informational mode. When the structure is complex, use nesting to attach a detailed template as an operand. When the desired format is easier to show than to describe, nest a sample output under Format (e.g., `### Example`).

**Constraints** — Constraints governs the response: what it contains, what it excludes, and what limits apply. Content to exclude ("omit disclaimers"), limits on recommendations ("budget: $500"), and requirements ("must include pricing") all belong here. If a constraint also describes work the AI should perform — *"research competitors and list the top five"* — split off the process step and place it in Task. Constraints should contain only rules about the finished output.

---

## Full Prompt Examples

### Shopping — Markdown (5 Directives)

```markdown
## Goal
Choose one wireless mouse to order today.

## Context
I have wrist pain.

## Task
Recommend a wireless mouse.

## Format
Product comparison with pros and cons for each, then a single recommendation.

## Constraints
Under $60, Amazon US, ergonomic only, Mac-compatible.
No gaming mice or trackballs.
```

This prompt omits Role — the Task and Constraints are specific enough without it. Goal clarifies that the output should lead to an immediate purchase decision, not a general product roundup.

### Kitchen Remodel — Markdown (6 Directives)

```markdown
## Goal
Choose one general contractor to remodel our kitchen by end of month.

## Role
Home renovation advisor

## Context
### Contractor Bids
- Martinez Renovations — bid $42,000, 4.8 stars (62 reviews)
- Summit Builders — bid $51,500, 4.6 stars (140 reviews)
- ClearView Construction — bid $38,000, 4.2 stars (28 reviews)

## Task
Evaluate the contractors on price, review quality,
and experience with older homes, and recommend one.

## Audience
Homeowners with no construction background.

## Format
Side-by-side comparison, then a ranked recommendation with reasoning.

## Constraints
Budget is $40,000–$55,000. Do not recommend based on lowest bid alone.
Omit generic advice about getting multiple quotes.
```

This prompt uses six directives and one data operand. "Contractor Bids" is a `###` sub-section under Context — it holds the static data the Task acts on. The evaluation criteria (*price, review quality, experience with older homes*) are in Task because they describe the work the AI performs. The budget restriction and content exclusion are in Constraints, where output rules belong.

---

*Directive conventions as of mid-2026. Reflects common practice across major AI platforms (Claude, ChatGPT, Gemini). Specific models may respond differently — test and iterate.*
