---
project: polyGo
version: 1
status: draft
created: 2026-05-25
context_type: greenfield
product_type: web-app
target_scale: small
timeline_budget:
  mvp_weeks: 8
  hard_deadline: 2026-07-25
  after_hours_only: true
---

## Vision & Problem Statement

polyGo is an online collaboration platform for the plastics industry — a trusted community that replaces cold calls, manual email outreach, and waiting months for trade fairs, with direct connections between verified companies and a self-populating database built from registrations.

The plastics sector has roughly 50,000 companies in Europe across plastic processing, raw materials, additives, and machinery. Finding the right partner, supplier, or client is difficult: online information is often limited or outdated, and meaningful connections mostly happen at periodic trade events (Fakuma, PRSE, Plastpol) that take place a few times a year. Between events, people rely on manual phone calls, email chains, and spreadsheets that nobody keeps up to date.

Existing online platforms for the plastics sector are transactional marketplaces — post an inquiry, receive a supply offer. They are not communities. polyGo is built around collaboration and direct communication. The database builds itself from verified company registrations; no one has to fill it manually. The verification layer is what makes every connection trustworthy. No fake accounts, no unknown entities — only real, confirmed companies.

## User & Persona

**Adam — Sales Specialist (38)**
Works full-time at a plastics recycling company. Responsible for maintaining relationships with existing clients and finding new ones. Spends significant time every day manually searching for potential partners online, verifying each lead individually, and communicating across email, phone, and WhatsApp simultaneously — often all three with the same counterpart. Loses track of agreements because communication is scattered. Maintains an internal database that he rarely has time to update. When a new material appears in his portfolio, he often doesn't know which clients to approach because his records are incomplete or outdated. He wants a platform where companies keep their own information current, so he can find what he needs without hunting.

**Nina — Office Worker / Order Manager (42)**
Works full-time at a plastics components manufacturer. Manages current orders and ensures the correct flow of information and documents between her company and its counterparts. Contacts many companies daily, each with a different organisational structure. At different stages of a transaction she needs to reach different people at the same company — and finding the right contact each time costs her time and causes errors. She is organised and values clarity; disorder stresses her. If a new tool requires days of learning, she abandons it and returns to familiar methods. She needs everything in one place and usable from the first session.

**Additional case studies from field research (PRSE Amsterdam, Plastpol Kielce):**
- A purchasing manager at a large multi-branch company in Poland who struggles to find materials with very specific properties, currently solving this by calling multiple suppliers one by one.
- A representative from Dopak who struggles to find companies that produce short-series runs — a need that has no reliable online search path today.

## Success Criteria

### Primary
Users give positive feedback that polyGo delivers real value in their daily work, and express that they see potential for more value as the platform grows.

### Secondary
Users begin inviting their own clients and partners to join polyGo. New registrations arriving through the invitation mechanism signal that the product has genuine product-market fit.

### Guardrails
- All conversations must be end-to-end encrypted. Users must be 100% confident that no one — including polyGo — can read their messages. This is a non-negotiable trust requirement; without it, users will not share business-sensitive information on the platform.
- The platform must have a flat learning curve. New users must be able to use core features from their first session without training, documentation, or onboarding calls. Complexity leads to abandonment (Nina persona).
- The instant messenger must work reliably at all times. Downtime, lag, or message loss sends users back to email and manual workflows — defeating the core purpose of the platform.

## User Stories

**Given** Adam has a new recycled material to offer but doesn't know which companies process it
**When** he searches polyGo by industry branch and material type
**Then** he finds a list of verified companies that may be interested and sends them a direct message via the built-in messenger — without making a single phone call

**Given** Nina needs to contact someone at a company she hasn't worked with before
**When** she opens that company's polyGo profile and identifies the right contact person
**Then** she sends a direct message through the messenger and starts the conversation immediately — without hunting for an email address or phone number

**Given** a purchasing manager needs a material with very specific properties
**When** he searches polyGo using the relevant filters
**Then** he finds verified suppliers that offer that material and contacts them directly — replacing a process that previously required calling multiple suppliers one by one

## Functional Requirements

- FR-001: A company can register on the platform by providing an email address, password, company description, logo, photos, and industry branch selection. Priority: must-have.
  *Confirmed essential — the company profile is the foundation of the self-building database.*

- FR-002: The polyGo platform admin can review each company registration and approve or reject it before the company gains access to the platform. Priority: must-have.
  *Confirmed essential — manual verification in v1 is the primary trust mechanism.*

- FR-003: A company admin can create user accounts for their own employees and manage those accounts (add, deactivate). Priority: must-have.
  *Confirmed essential — companies like Nina's require multiple users from day one; one shared login is not viable.*

- FR-004: A logged-in user can search for companies on the platform by industry branch and other available criteria. Priority: must-have.
  *Confirmed essential — discovery is the core value proposition.*

- FR-005: A logged-in user can view the full profile of any verified company on the platform. Priority: must-have.
  *Confirmed essential — profiles are the information layer that replaces cold research.*

- FR-006: A logged-in user can initiate a direct message conversation with a user at another verified company via the built-in instant messenger. Priority: must-have.
  *Confirmed essential — the messenger is the primary reason users have to return to polyGo daily.*

- FR-007: Users can conduct real-time, end-to-end encrypted text conversations through the built-in messenger. Priority: must-have.
  *Confirmed essential — encryption is a hard requirement; messenger reliability is a guardrail.*

- FR-008: A company admin can update their company's profile information, photos, and logo after the initial registration. Priority: must-have.
  *Confirmed essential — outdated profiles defeat the self-building database premise; the value of the platform depends on profiles staying current.*

- FR-009: The polyGo platform admin can moderate content and manage companies and users across the platform. Priority: must-have.
  *Confirmed essential — platform integrity requires admin oversight.*

## Non-Functional Requirements

- NFR-001: All messenger conversations are end-to-end encrypted. No party, including polyGo, can access message content.
- NFR-002: The platform must have a flat learning curve. New users must be able to use core features from their first session without training, onboarding calls, or documentation.
- NFR-003: The instant messenger must be reliable and responsive. Service degradation or message loss is not acceptable for the primary use case.
- NFR-004: The platform must comply with GDPR requirements applicable in Poland and the European Union.
- NFR-005: The MVP is available in Polish only. The platform architecture must support multi-language expansion from the start. Polish + English is the v2 target; Italian, French, and German are planned for the European market rollout.
- NFR-006: Mobile access is a long-term goal (messenger functionality only) and is not required for MVP.

## Business Logic

Given a user's industry branch and search criteria, polyGo surfaces verified, real companies from the plastics sector that match — companies the user may not have known existed, that cannot be reliably found through a standard web search, and that would otherwise require attending a trade fair or relying on a personal introduction to reach.

The verification layer is what makes each match trustworthy: every company visible on the platform has been manually confirmed by the polyGo platform admin. The database is self-populating — companies register and maintain their own profiles, so the information stays current without any central effort. This is what differentiates polyGo from a static directory, a marketplace, or a spreadsheet: the data is live, the companies are verified, and the connection is one message away.

## Access Control

**Registration and verification:**
Companies register with email and password (no social login in v1). Each registration undergoes manual review and approval by the polyGo platform admin before the company and its users gain any access. Invitation by existing verified members is a planned v2 feature; when implemented, the "invited by" relationship will be traceable for trust reference purposes.

**Roles:**

| Role | Who | What they can do |
|---|---|---|
| polyGo platform admin | polyGo team | Verify and reject registrations, moderate content, manage all companies and users on the platform |
| Company admin | One designated person per company | Manage the company profile, create and manage employee user accounts within their company |
| Company user | Employees added by the company admin | Search for companies, view profiles, send and receive messages via the instant messenger |

## Non-Goals

The following are explicitly out of scope for v1:

- **Not a marketplace:** polyGo does not facilitate buy/sell inquiries, purchase orders, price negotiations, or any transactional layer. It connects people; it does not process deals.
- **No external integrations:** No ERP, CRM, email client, or third-party messaging app (e.g. WhatsApp) integrations in v1. polyGo stands as a standalone platform.
- **No market analytics:** No dashboards, trend reports, pricing intelligence, or sector statistics in v1.
- **Polish market only:** Companies outside Poland are not onboarded in v1. European expansion follows successful MVP validation in Poland.

## Open Questions

1. **Document sharing in messenger:** Confirmed as v2 priority. End-to-end encryption requirements will apply equally to documents. Scope and format (file types, size limits) to be defined before v2 development begins.
2. **Invitation system:** Moved to v2. When implemented, the "invited by" relationship must be traceable so polyGo can request references from the inviting company if needed.
3. **Mobile app:** Long-term goal, limited to messenger functionality. Timeline and scope to be decided after MVP is live and validated.
4. **Multi-language support:** Polish only in MVP. Polish + English in v2. Full European language support (Italian, French, German) as part of European market expansion planning.
5. **Authentication details:** Email + password confirmed for v1. Specific session management, password reset flow, and security standards to be decided during technical design.
6. **Search and filtering depth:** The MVP requires search by industry branch. The full set of searchable criteria (material type, geography, company size, etc.) has not been defined — to be scoped before development of FR-004 begins.
7. **MVP launch timeline:** 8-week target from 2026-05-25 (target: ~2026-07-25). After-hours project; exact technical timeline to be agreed with the technical co-founder.
