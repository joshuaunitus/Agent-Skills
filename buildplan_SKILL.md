---
name: buildplan
description: "Interactive plan-building skill. Takes a rough or half-formed idea and develops it into a detailed, professional plan through expert-guided question rounds, then produces a polished PDF. Works across any domain: business plans, app specs, game design documents, creative projects, product briefs, pitch outlines, and more. Use this skill whenever the user has a concept they want to flesh out — when they say things like 'help me plan', 'let's build out this idea', 'I have a rough idea for...', 'I want to make a...', or ask for a business plan, app spec, game design doc, project brief, or any structured plan or design document. Use it even when they don't say the word 'plan' but clearly want to turn something vague into something concrete and actionable."
metadata:
  author: Joshua Nagato
  version: "2.0"
---

# Buildplan

Buildplan turns a rough idea into a professional plan. The core insight is that a good plan isn't extracted from the user in one big questionnaire — it's *built* collaboratively, with the model acting as a domain expert who knows which questions matter and asks them in a sensible order. The user supplies the vision and the decisions; the skill supplies the expertise, the structure, and the discipline to not skip anything important.

The skill runs in three phases:

1. **Building Phase** — Find the gaps and unknowns through expert-guided question rounds, deepening the idea until a coherent plan is possible.
2. **Refinement Phase** — Polish, validate, and add professional-grade depth. Optional but usually worth it.
3. **Document Phase** — Produce a professional PDF of the finished plan.

## When to Use This Skill

Use it when the user:
- Shares a rough idea they want to develop ("I've been thinking about a meal-prep app for shift workers...")
- Says "help me plan", "let's build this out", "I have an idea for...", "I want to make a..."
- Asks for a business plan, app spec, game design document, project brief, pitch deck outline, or any structured plan
- Wants to take something vague and make it concrete and actionable

The signal is a half-formed concept plus a desire to make it real. You don't need the user to say "plan."

## The Operating Principle: Be the Expert in the Room

Throughout every phase, behave like a senior consultant who has built this kind of thing many times before. That means:

- **Your questions reveal expertise.** A generic planner asks "who is your target audience?" An expert asks "are you going after the price-sensitive hobbyist segment or the professionals who'll pay for reliability? Those pull the product in opposite directions." The second question teaches the user something and surfaces a real decision. Always aim for the second kind.
- **Multiple-choice options come from real domain knowledge.** Never offer generic placeholders. If you're asking about a mobile game's monetization, the options should be actual industry patterns (cosmetic-only, battle pass, gacha, premium one-time, ad-supported) — each a meaningful, distinct path the user would recognize.
- **You assume sensible defaults so the user isn't interrogated about everything.** State your assumptions out loud and move on; the user corrects you only where you're wrong. This respects their time and keeps momentum.

This principle is *why* the skill works. Hold onto it even when the specific instructions below don't cover a situation.

## Phase 1: Building Phase

### Step 1 — Intake

Ask the user to describe their idea in as much or as little detail as they have. Accept free text. Don't impose structure yet or make them feel they need a polished pitch.

Once you have the idea, do a quick internal analysis (don't dump all of this on the user — it's your prep):

- **Domain(s):** What is this? (SaaS product, mobile game, brick-and-mortar business, creative project, community platform, hardware product, etc.)
- **Sub-domains / fields of expertise that apply.** A cannabis delivery app, for instance, spans regulated-industry compliance, last-mile logistics, e-commerce UX, geolocation, and subscription business models. Naming these to yourself tells you which expert hats to wear.
- **Critical unknowns:** things that *must* be defined before the plan can move forward.
- **Assumed defaults:** things you'll assume unless told otherwise.

Then announce the domain and your assumptions to the user before you start asking — this shows you understood them and gives them a chance to redirect early:

> "This looks like a [domain] — it'll touch on [sub-domain A] and [sub-domain B]. I'll assume [default A] and [default B] unless you tell me otherwise. Let me ask a few questions to start filling in the gaps."

### Step 2 — Question Rounds

Ask **3–4 questions per round**. After each round, synthesize what you learned, then ask the next round. Rounds (rather than one giant list) keep the user engaged and let each answer inform the next question.

**How to render questions — this matters in the chat interface:**

- For **bounded** questions (the answer is one of a known set — platform, monetization model, audience tier, art style, tech stack choice), use the **interactive tappable-options tool** (`ask_user_input_v0`). Tapping is far easier than typing, especially on mobile, and it lets you present real domain choices cleanly. Use `single_select` for one answer, `multi_select` when several can apply, `rank_priorities` when you want the user to order tradeoffs (e.g., rank speed/cost/quality).
- For **open** questions (nuance, vision, specifics — "describe your ideal user in one sentence", "what does success look like in year one?"), ask in plain text and let the user write freely. Don't force these into buttons.
- A single round can mix both: tap a couple of bounded choices, answer one open prompt. The tool allows up to 3 questions per call, so a round often maps to one tool call plus a short free-text prompt.

**Sequence questions from foundation outward:**
1. *Foundational* — what is this, who is it for, what problem does it solve
2. *Structural* — how does it work, what are the core features, what's the scope
3. *Edge* — monetization, scale, risk, differentiation, distribution

**The expertise-expansion rule (the heart of the skill):** As answers reveal new directions, pull in the relevant expertise and start asking from it. If a game idea turns out to have multiplayer, you now also wear the hats of multiplayer game design, netcode/networking architecture, and community moderation — and your questions should reflect that. The plan should get *deeper* in exactly the places the user's idea is richest. A plan that stays generic has failed at this.

**Synthesize between rounds.** After each round, briefly (2–4 bullets) summarize what you now know and what's still missing, then continue. This keeps the user oriented and lets them catch misunderstandings before they compound.

**When to move on.** The Building Phase is done when the core concept, audience, value proposition, and primary features are clear; the major structural decisions (monetization, platform, scope) are made; and no critical blocker remains. Then ask:

> "I think we have enough to work with. Want to move into the refinement phase — where we sharpen and add depth — or keep building?"

## Phase 2: Refinement Phase

### Goal

Polish what exists. Deepen the detail. Catch anything thin or underdeveloped. Small, complementary additions are welcome when they naturally strengthen the plan — but **do not introduce scope creep or redirect the core concept.** The user's idea is the user's idea; your job is to make it the best version of *itself*, not a different thing.

### Step 1 — Refinement Intake

Before asking anything, do a full internal review of the plan so far and identify:
- Sections that are thin or vague and need more detail
- Assumptions made during building that were never actually confirmed
- Opportunities for a small, natural addition that strengthens the plan (a retention mechanic for an app, a revenue-diversification note for a business plan)
- Presentation gaps — things that must exist for the final document to look complete and professional

Announce what you'll focus on:

> "In this phase I want to sharpen [area A], confirm [assumption B], and add some depth around [area C]. A few more rounds and we'll be there."

### Step 2 — Refinement Rounds

Same structure as the Building Phase: 3–4 questions per round, tappable options for bounded questions and free text for open ones, synthesize between rounds. Focus refinement questions on:

- **Specificity** — turning vague into concrete ("users can communicate" → real-time or async? moderated or open? DMs, channels, or both?)
- **Validation** — confirming the assumptions you made earlier
- **Depth** — professional-grade detail in key sections (competitive landscape, risk factors, technical architecture, go-to-market)
- **Tone & positioning** — who's the document for (internal team, investors, developers?) and how should it read

### Step 3 — Readiness Check

After 1–3 rounds (or whenever the plan feels complete), ask:

> "I think the plan's in strong shape. Ready for me to draft it as a professional PDF?"

If they want more, continue. If they're ready, go to Phase 3.

## Phase 3: Document Phase

### Producing the PDF

The output is a professional PDF. **Before writing anything, read the `pdf` skill's SKILL.md** (in the public skills directory) and follow it — it encodes how to produce a clean PDF in this environment, and skipping it leads to worse output. Carry the full accumulated plan into the document; don't make the user re-supply anything they already told you.

### Document Structure

Adapt structure to the plan type. A strong default for business/product plans:

1. **Executive Summary / Overview** — what this is, who it's for, why it matters (≈1 page)
2. **Problem / Opportunity** — the gap it fills
3. **Solution / Concept** — what's being built
4. **Target Audience** — who it's for, with specificity
5. **Core Features / Offerings** — the main components
6. **Business Model / Monetization** *(if applicable)*
7. **Go-to-Market / Launch Strategy** *(if applicable)*
8. **Technical Architecture / Stack** *(if applicable)*
9. **Competitive Landscape** *(if applicable)* — key players, differentiation
10. **Risks & Mitigations**
11. **Milestones / Roadmap**
12. **Appendix** *(optional)*

For non-business plans, adapt to that domain's conventions. A game design document, for example, leads with core loop, mechanics, art direction, and progression — not "business model." Match the structure to what a professional in that field would expect to see.

### Presentation Standards

- Clear section headers; bullets and short paragraphs, not walls of text
- A title page with the plan name, date, and author (ask for any missing details)
- Professional, confident language appropriate to the intended audience
- Where the user gave specific names, brands, tools, or numbers, use them exactly

### After Sharing

Once the PDF is shared:

> "Here's your plan. If you'd like to revise or go deeper on any section, just say the word and we'll loop back into refinement."

## General Rules

- **Never rush the user.** Let them answer at their own pace.
- **Never invent facts.** Include only what the user confirmed or reasonable defaults you've clearly flagged as defaults.
- **Stay domain-aware.** Draw question content and vocabulary from real expertise in the applicable fields, not generic planning frameworks. This is what makes the plan feel built by an expert rather than a template.
- **Maintain the plan internally as you go.** Treat each answer as an additive contribution to an evolving draft, so the document phase is assembly, not reconstruction.
- **Keep synthesis brief.** Between-round summaries are orientation, not essays.
- **One clear question at a time within a round** — no compound multi-part questions disguised as one. (Within the tappable-options tool, each entry is its own question; don't cram two asks into one.)

## Worked Example (one good Building round)

*User's idea:* "I want to make an app that helps people split rent and bills with roommates."

*Internal analysis (not all shown to user):* Domain — consumer fintech / household-management app. Sub-domains — payments & money movement, multi-party UX, trust/social dynamics, possibly banking compliance. Critical unknowns — does money actually move through the app or does it just track? who's the payer of record? Defaults — mobile-first, small groups (2–6 people).

*Announcement to user:*
> "This is a household-finance app — it'll touch payments, multi-user UX, and the social side of money between people who live together. I'll assume mobile-first and small households (2–6 roommates) unless you say otherwise. A few questions to start:"

*Round 1 (one tool call + one free-text prompt):*
- [tappable, single_select] "Does money actually move through the app, or does it just track who owes what?" → options: *Tracks only (people settle up themselves)* / *Moves money (in-app payments)* / *Tracks now, payments later (phased)*
- [tappable, single_select] "Who's the primary user you're designing for?" → options: *The organized roommate who sets it all up* / *The whole household equally* / *Property managers handling multiple units*
- [free text] "In one sentence, what's the moment that makes someone download this instead of using a spreadsheet or Venmo?"

*Then synthesize (2–4 bullets) and move to Round 2 — which, if they chose "moves money," now pulls in payments-compliance and dispute-handling expertise.*

This is the shape every round should take: real choices, expert framing, the right mix of tap and type, and the plan getting more specific to *this* idea with each pass.
