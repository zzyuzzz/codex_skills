---
name: principle-explainer-topics
description: Create topic ideas for principle-explainer creators in technology and economics. Use when Codex needs to propose, prioritize, or justify content topics; turn research papers, arXiv posts, top conferences, journals, policy changes, or economic releases into explainable story ideas; or package those ideas into article, thread, or video angles.
---

# Principle Explainer Topics

## Overview

Use this skill to help a creator find topics worth explaining, not just topics that are new. Favor ideas that reveal a mechanism, correct a common misunderstanding, or help the audience reuse one principle across many events.

## Workflow

### 1. Clarify the request mode

Identify which mode best matches the user's request:

- `broad-ideation`: Generate a batch of candidate topics from technology, economics, or both.
- `paper-led`: Start from papers, preprints, journals, or conferences.
- `news-led`: Start from current events, policy moves, data releases, or public debate.
- `planning-led`: Build a weekly or monthly slate with a balance of timely and evergreen topics.

If the user does not specify a mode, infer the most likely one and proceed.

### 2. Gather source signals

Build a short candidate list from one or more signal groups:

- Technology research: arXiv, conference proceedings, lab blogs, model evaluations, benchmark reports
- Economics research: NBER, working papers, journals, central bank research, IMF/OECD/World Bank reports
- Public triggers: major product launches, regulation, market moves, headline debates, surprising data prints
- Durable confusion: topics people repeatedly misunderstand, oversimplify, or frame as binaries

Read [references/source-map.md](references/source-map.md) when the user wants concrete source families or paper-hunting guidance.

### 3. Score for explanation value

Do not default to novelty. Score each candidate on the six factors below, using a simple 1-5 or 1-10 scale:

- `relevance`: Does the audience already care or soon need to care?
- `explanation_value`: Is there a real mechanism to unpack?
- `transfer_value`: Will learning this help explain other cases later?
- `timeliness`: Is there a current trigger or discussion window?
- `differentiation`: Can this angle go beyond obvious summaries?
- `evidence_strength`: Can the argument be grounded in papers, data, or primary sources?

Prefer topics that explain a bigger pattern through a smaller event.

### 4. Turn each topic into a principle-first angle

For every strong candidate, frame it with this structure:

- `phenomenon`: What people are seeing right now
- `misread`: What most people get wrong
- `mechanism`: The 1-3 principles that actually drive the outcome
- `evidence`: Papers, data, institutional reports, or historical comparisons
- `extension`: What else this principle helps explain
- `takeaway`: The belief the audience should update

If the topic is still too newsy, rewrite it until the mechanism is the center of gravity.

### 5. Package for format

Unless the user asks otherwise, provide at least one packaging angle:

- `article`: Best for layered explanation and evidence
- `thread/post`: Best for testing the hook and framing
- `video`: Best for explaining one mechanism with examples

Note whether the idea is best as:

- `searchable`: answers an existing question
- `shareable`: offers a surprising or contrarian insight
- `both`

## Paper-Led Rules

When starting from papers, prioritize work that is not only academically interesting but also explainable to non-specialists. Prefer papers that:

- challenge a common belief
- introduce a mechanism with broad real-world relevance
- clarify a hot topic that is otherwise being discussed shallowly
- connect technical change to economic or social outcomes

Avoid paper ideas that depend on narrow jargon, tiny incremental gains, or results that cannot survive simplification.

## Output Format

Use this structure unless the user requests another format:

- `topic`
- `one-line angle`
- `why it is worth covering`
- `core principle`
- `supporting evidence to look for`
- `best format`
- `difficulty`
- `timeliness`
- `do now / later / skip`

When giving multiple ideas, rank them strongest first.

## Defaults

- Prefer "small topic, big explanatory payoff" over "big headline, thin explanation".
- Favor primary sources over commentary.
- If using current developments, distinguish clearly between the event and the principle.
- If a topic is trendy but weakly evidenced, say so and lower its priority.

## Example Requests

- "Use $principle-explainer-topics to give me 10 technology topics with strong explanatory value."
- "Use $principle-explainer-topics to turn recent arXiv papers into creator-friendly ideas."
- "Use $principle-explainer-topics to build a weekly slate mixing AI, macroeconomics, and policy."
- "Use $principle-explainer-topics to find economics topics that are timely but still evergreen."
