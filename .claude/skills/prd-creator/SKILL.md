# /10x-prd-biz — Guided PRD Discovery for Non-Technical Users

This skill walks a non-technical, business-focused user through the full
discovery process and produces a finished `context/foundation/prd.md`.
No prior knowledge of product terminology is required. No other skills
are needed — this skill is self-contained.

**Output:** `context/foundation/prd.md` (one file, no intermediaries)

---

## When to use

Use when a business-focused user wants to go from idea → structured PRD
without knowing product or engineering terminology. Greenfield only
(building something new from scratch).

Skip when the user is technical and comfortable with `/10x-shape` +
`/10x-prd` directly.

---

## Plain-English term reference

Whenever one of these terms must surface in a user-facing message,
use the plain-English version. Never use the technical term alone
on first appearance.

| If you must reference... | Say instead... |
|---|---|
| functional requirement | something the user must be able to do |
| user story | a short description of one action and its result |
| business logic | the decision your product makes that a spreadsheet couldn't |
| non-functional requirement | a quality commitment (speed, privacy, reliability) |
| non-goal | something this version is explicitly NOT doing |
| MVP | the smallest version that proves the product works |
| PRD | Product Requirements Document — a structured description of what to build and why |
| greenfield | building something new from scratch |
| success criteria | how you'll know the product worked |
| access control | who gets in and what they can do |

---

## Process

### Initial response

When invoked with an idea inline (e.g. `/10x-prd-biz a tool that helps
sales teams track follow-ups`), capture it verbatim as the seed idea
and proceed to Step 0.

When invoked with no argument, respond with:

```
I'll guide you through building a Product Requirements Document (PRD) —
a structured description of what you want to build and why.

We'll go through 7 short phases of questions. You answer in plain language;
I handle the structure. No technical knowledge needed.

To start: what do you want to build? One or two sentences is enough.
```

Then wait.

---

### Step 0 — Folder setup

Run silently:

```bash
mkdir -p context/foundation
```

Check for an existing PRD:

```bash
test -f context/foundation/prd.md
```

If found, tell the user:

```
I found an existing PRD at context/foundation/prd.md.
```

Then ask:

AskUserQuestion:
- question: "What would you like to do?"
- options:
    - "Save the new PRD as a numbered backup (e.g. prd-v2.md) — keeps both (Recommended)"
    - "Overwrite the existing PRD — the old version will be lost"
    - "Cancel — exit without changes"

Store the collision choice. Proceed to Step 1 regardless of choice
(the write destination is resolved at the end in Step 8).

---

### Step 1 — The problem

**Goal:** understand who has the pain, what it is, and what it costs today.

Open with: "Let's start with the problem your product solves.
In a sentence or two — who has it, when do they feel it, and what does
it cost them today?"

Listen. Echo back four things:

```
The pain:        [the actual problem]
Who has it:      [a specific type of person or role — not "everyone"]
When it happens: [the moment or situation that triggers it]
Cost today:      [what they do now, and what that costs them]
```

If any of the four is vague ("everyone", "all the time", "really painful"),
ask one focused follow-up: "Who specifically have you seen experience this
in the last month — can you name a role or type of person?"

Then ask:

AskUserQuestion (multi-select):
- question: "What kind of problem is this? Pick everything that fits."
- options:
    - "Something that wastes too much time"
    - "Something people can't do at all today"
    - "Information that's stuck somewhere it can't be used"
    - "Hard to make the right decision without better tools"
    - "Too much coordination needed between people"
    - "Something else — I'll describe it"

Also ask in a follow-up message: "If this idea is so useful, why hasn't
someone built it already? What do you know that others don't?"
Capture the answer — it's the product's core insight.

Store as: `vision_statement`, `primary_persona`, `problem_insight`.

---

### Step 2 — Who gets in and how

**Goal:** capture access model and user roles.

Open with: "How does someone get into this product?"

AskUserQuestion:
- question: "How does a user access the product?"
- options:
    - "They log in with email/password or Google/social login (Recommended for most web products)"
    - "It lives on their device — no login, no server"
    - "They get a link or a key — no account needed"
    - "No access control — single user, no separation needed"

If anything other than single-user, follow up:

AskUserQuestion:
- question: "Once they're in, is everyone the same — or are there different types of users who see different things?"
- options:
    - "Everyone is the same — no roles needed (Recommended for simple first versions)"
    - "There are 2–3 roles with different permissions — I'll describe them"
    - "Not sure yet"

If roles exist, ask: "Describe each role in one sentence — who they are
and what they can do that others can't."

Store as: `access_model`, `roles`.

---

### Step 3 — The smallest version that proves this works

**Goal:** pin MVP scope and timeline. Surface cost honestly if scope is large.

Open with: "Walk me through the first time someone uses this — step by
step, from the moment they open it to the moment they get value.
What do they do?"

Listen. Echo back as a numbered list. Then ask:
"If you had three weeks of evenings and weekends, could you ship this?"

**If scope is too large** (more than ~6 steps before the user gets value,
or the user's own estimate significantly exceeds 3 weeks, or the flow
requires multiple external services before anything works):

```
What you've described is bigger than what typically ships in three weeks
of after-hours work. The most common reason first versions never ship is
that the first version was too ambitious to finish.

Two honest options:

  Cut the scope — keep the timeline short. For example:
    - Drop [the expensive piece] for v1; add it once v1 ships.
    - Replace [the integration] with a manual workaround for now.
    - Limit v1 to just yourself, then open it up.

  Commit to the longer timeline — totally valid, but go in eyes-open.
  A multi-week after-hours project requires sustained effort over evenings
  and weekends. Most projects that exceed their first estimate don't fail
  from the work itself — they fail from the gap between expected and
  actual effort.
```

AskUserQuestion:
- question: "How do you want to handle the scope?"
- options:
    - "Cut the scope — let's find the smallest version that proves this (Recommended)"
    - "Commit to the longer timeline — I understand what that means"
    - "Let me re-describe the first version from scratch"

If "Commit": ask for estimated weeks. Store an acknowledgment:
`Acknowledged <YYYY-MM-DD>: <N>-week MVP, user accepted the cost.`
Do not repeat the warning after this point.

After scope is locked, ask for success criteria:

- "How will you know this worked? Describe the moment of success."
  → primary success criterion
- "What's one nice-to-have on top of that?"
  → secondary criterion
- "What must definitely NOT get worse or break?"
  → guardrails

Store as: `mvp_flow`, `mvp_weeks`, `success_primary`, `success_secondary`,
`success_guardrails`.

---

### Step 4 — What users must be able to do

**Goal:** capture functional requirements and at least one user story.

Open with: "Now let's get specific. From the flow you described, what
must users be able to do? List the capabilities — just plain language,
I'll handle the formatting."

Capture each capability internally as:
`- FR-NNN: [Actor] can [capability]. Priority: must-have | nice-to-have`

NNN is zero-padded, starting at 001. Default to must-have for anything
in the MVP flow; ask explicitly if anything feels optional.

Echo capabilities back to the user as a plain numbered list for
confirmation — never show FR-NNN syntax.

Group thematically with subheadings if more than 6 capabilities.

Then introduce user stories — say this once:
"For the main flow, let's write a short description of it from the
user's perspective. It follows a simple pattern:
Situation → Action → Result.

Example:
Situation: a sales rep just finished a call
Action: they log the outcome in the tool
Result: the tool schedules a follow-up reminder automatically

Walk me through your main flow in that format."

Capture at least one story for the primary flow. Additional ones are
optional but encouraged for anything with a non-obvious outcome.

Format internally as Given/When/Then:
```
**Given** [situation]
**When** [action]
**Then** [result]
```

Store as: `functional_requirements[]`, `user_stories[]`.

---

### Step 4.5 — Pressure-test each capability

**Goal:** challenge each capability with a "what could go wrong" question.
Catch scope creep before it's too late.

Tell the user:
"Now let's pressure-test each capability. For each one I'll ask: what's
the strongest argument for leaving this OUT of the first version?"

For each capability in order, generate one specific challenge
(not generic). Always put "No — this belongs in v1" as the last option.

Example for "User can save items to favorites":

AskUserQuestion:
- question: "Favorites — is this truly needed in v1?"
- options:
    - "Maybe not — if the list is short, favorites add no value yet"
    - "Maybe not — could add in v2 once we see how people use it"
    - "No — this belongs in v1"

If the user's response prompts a change (drop, downgrade, split),
update the capability in place.

Store each response as a note alongside its capability.

---

### Step 5 — The decision your product makes

**Goal:** capture the one rule the product applies that a spreadsheet
couldn't. This is the most important section — a product without a
decision is just a data store.

Open with: "Here's an important question: what decision does your product
make for the user that a spreadsheet or a notes file couldn't?
Describe it in one sentence."

If the user struggles, offer shapes:

AskUserQuestion (multi-select):
- question: "What does your product DO for the user — beyond storing data?"
- options:
    - "It recommends something based on their situation"
    - "It prioritizes or ranks things for them"
    - "It classifies or tags things automatically"
    - "It checks something against a rule and flags problems"
    - "It calculates a value from inputs they give"
    - "It moves things through a defined process step by step"
    - "Honestly, it just stores and retrieves data — no real decision"

If "just stores and retrieves data":

```
What you've described stores data but doesn't make any decisions.
That means your product provides no value a spreadsheet couldn't —
and products that just store data tend not to get used after the
first week.

A product that makes a decision — recommends, prioritizes, classifies,
validates, calculates, or moves things through a process — gives users
a reason to keep coming back.

What decision could your product make?
```

Use AskUserQuestion with the rule shapes above. If they still choose
"just storing data", record `# TODO: domain rule — see Open Questions`
and add an Open Questions entry. Do NOT invent a rule.

After the rule is stated, ask for up to 3 supporting details:
- What inputs does the rule use? (describe as user-facing inputs, not
  system components)
- What does it produce for the user?
- Where in the product flow does the user encounter it?

Then ask about quality commitments:
"Are there any quality commitments this product must keep — things a
user or regulator could observe from the outside?"

Give examples: "Loads in under 2 seconds. Works on mobile. Doesn't
store personal data without consent. Available 99% of the time."

If the user phrases a commitment mechanically (e.g. "rate-limit per IP",
"Postgres query under 50ms"), reflect it back in observable form:
"Got it — so the product resists abuse without locking out legitimate
users / responds in under a second as the user experiences it?"

Store as: `business_rule`, `nfrs[]`.

---

### Step 6 — Framing and what you're NOT building

**Goal:** pin product type, scale, timeline facts, and explicit non-goals.

Open with: "Last phase — three quick questions, then we'll lock down
what this version is explicitly NOT doing. No technology decisions here —
those come after the PRD."

Ask three questions, one at a time:

**1.**
AskUserQuestion:
- question: "What kind of thing are you building?"
- options: "A website or web app" / "An API or backend service" /
  "A command-line tool" / "A mobile app" / "A desktop app" /
  "A library or toolkit" / "A data pipeline" / "Something else"

Map internally: web-app / api / cli / mobile / desktop / library /
data-pipeline / other → `product_type`.

**2.**
AskUserQuestion:
- question: "Roughly how many people will use this once it's live?"
- options: "Just me, or a handful" / "Dozens to a hundred" /
  "Up to ten thousand" / "More than ten thousand"

Map internally: small / medium / large / enterprise → `target_scale`.

**3.**
Ask in one message: "Is there a hard deadline you're aiming for?
And is this after-hours work or part of your day job?"

Map to: `hard_deadline` (ISO date or null), `after_hours_only` (bool).

**Non-goals:**

Tell the user: "Now let's protect the scope. What is this first version
explicitly NOT doing? Naming non-goals upfront prevents scope creep and
sets clear expectations."

AskUserQuestion (multi-select, 4–5 options generated from the user's
specific domain — not generic):

Generate options in these shapes:
- "Not building our own [domain algorithm] — using an existing solution or skipping it"
- "Not supporting [secondary use case or persona] in this version"
- "Not aiming for [quality dimension — e.g. offline use, full accessibility] in v1"
- "Not integrating with [specific external system] yet"
- "Other — I'll describe it"

If technology avoids come up ("avoid PHP", "no AWS"), acknowledge them
but do NOT add to non-goals: "Good to know — I'll note that for the
technology selection step, which comes after the PRD."

Store as: `product_type`, `target_scale`, `timeline`, `non_goals[]`.

---

### Step 7 — Review before writing

**Goal:** surface any gaps before generating the PRD.

Run a check on everything captured. Report in plain language:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  REVIEW BEFORE GENERATING YOUR PRD
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  The problem:              [✓ captured | ✗ missing]
  Who gets in and how:      [✓ captured | ✗ missing]
  Smallest working version: [✓ captured | ✗ missing]
  What users can do:        [✓ N capabilities | ✗ missing]
  The product's core rule:  [✓ captured | ✗ missing — HIGH RISK]
  Quality commitments:      [✓ captured | ✗ none yet]
  What you're NOT building: [✓ N items | ✗ missing]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

For each missing item, name the consequence in plain language.
"The product's core rule is missing — the PRD will describe a data
store, not a product."

AskUserQuestion:
- question: "How do you want to proceed?"
- options:
    - "Fix the gaps now — take me back (Recommended if multiple items missing)"
    - "Continue anyway — I'll fill gaps in later"
    - "Go back to a specific phase"

On "Fix": ask which gap; return to the relevant step; come back to Step 7.
On "Continue": note all gaps. They will appear as open questions in the PRD.

---

### Step 8 — Write the PRD

**Goal:** assemble and write `context/foundation/prd.md` from everything
captured. This step runs silently — no more questions unless a critical
gap is discovered.

Get today's date:
```bash
date +%Y-%m-%d
```

Assemble the PRD content in memory using the schema below.
For every field or section where the user provided content — use their
exact words (reformat only when schema requires a specific shape).
For every field or section where content is missing — emit
`# TODO: [field] — see Open Questions` and add a numbered entry to
`## Open Questions`.

**PRD schema (greenfield, 10 sections in this exact order):**

```markdown
---
project: [from seed idea or Step 1]
version: 1
status: draft
created: [YYYY-MM-DD]
context_type: greenfield
product_type: [from Step 6]
target_scale: [from Step 6]
timeline_budget:
  mvp_weeks: [from Step 3]
  hard_deadline: [from Step 6 or null]
  after_hours_only: [from Step 6]
---

## Vision & Problem Statement

[vision_statement from Step 1]
[problem_insight from Step 1]

## User & Persona

[primary_persona from Step 1]

## Success Criteria

### Primary
[success_primary from Step 3]

### Secondary
[success_secondary from Step 3]

### Guardrails
[success_guardrails from Step 3]

## User Stories

[user_stories[] from Step 4 — in Given/When/Then format]

## Functional Requirements

[functional_requirements[] from Step 4 — in FR-NNN format]
[each FR followed by its Socrates blockquote from Step 4.5]

## Non-Functional Requirements

[nfrs[] from Step 5]

## Business Logic

[business_rule from Step 5]

## Access Control

[access_model and roles from Step 2]

## Non-Goals

[non_goals[] from Step 6]

## Open Questions

[numbered list of all TODOs and unresolved gaps]
```

**Pre-write self-check:**

Before writing to disk, verify:
- All 10 `##` sections are present, in order, exact spelling
- Frontmatter has all 8 required keys
- `## Success Criteria` has all three `###` subsections
- No vendor names, schema notation, runtime locations, or protocol
  names have leaked into sections other than what the user explicitly
  said (if found, move to Open Questions)

If any check fails, report what's wrong and fix in memory before writing.

**Write to disk:**

Resolve the destination from Step 0:
- No prior file → write to `context/foundation/prd.md`
- "Save as backup" chosen → scan for existing `prd-vN.md` files,
  write to next available slot (treat `prd.md` as v1, so first backup
  is `prd-v2.md`), bump `version:` frontmatter field to match
- "Overwrite" chosen → write to `context/foundation/prd.md`,
  keep `version: 1`

```bash
# ensure directory exists
mkdir -p context/foundation
```

Write the assembled content to the resolved path.

**Confirm to the user:**

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  YOUR PRD IS READY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Project:          [name]
  File:             context/foundation/prd.md
  Capabilities:     [N] defined
  Open questions:   [count] — things to resolve before building

  Fully captured:
    [list sections with real content]

  Needs your input later (open questions in the PRD):
    [list sections with TODOs]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Next step: /10x-tech-stack-selector
It picks the technology for what you've just described.
Run it when you're ready.
```

STOP. Do not chain automatically.

---

## Critical guardrails

**Never invent content.** If the user hasn't said it, don't write it.
Missing content → Open Questions. The business rule section is the most
policed: if no one-sentence rule was captured, it reads
`# TODO: domain rule — see Open Questions`. No exceptions.

**Never pick a tech stack.** No framework, database, hosting platform,
or language in any question or in the PRD. If the user volunteers
technology preferences, acknowledge and note: "I'll flag that for the
technology selection step after the PRD."

**Schema is the contract.** The 10 sections, their names, and their
order are fixed. The frontmatter keys are fixed. Do not add, remove,
or rename sections.

**Plain language throughout.** Technical terms from the reference table
never appear without their plain-English explanation on first use.
After the first explanation, prefer the plain version.

**Never chain automatically.** The hand-off to `/10x-tech-stack-selector`
is an announcement, not an invocation.