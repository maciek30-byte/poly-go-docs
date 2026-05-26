---
project: polyGo
version: 1
status: draft
created: 2026-05-26
updated: 2026-05-26
prd_version: 1
main_goal: quality
top_blocker: none
---

# Roadmap: polyGo

> Derived from `context/foundation/prd.md` (v1) + auto-researched codebase baseline.
> Edit-in-place; archive when superseded.
> Slices below are listed in dependency order.

## Vision Recap
Polish plastics companies lack a reliable way to verify new commercial counterparties — public listing portals are flooded with fakes, and daily communication is dispersed across private channels. **polyGo** trades scale for trust: a 10+ year industry insider manually verifies every company. Manual gatekeeping and the platform's closed nature *are* the moat.

## North Star
**S-06: 1:1 chat with phone reveal.**
An Employee opens a 1:1 chat with a counterparty's Employee, exchanges text messages with read-receipts, and the counterparty's phone number is revealed upon opening the conversation with an audit log. This is the core success criterion for the MVP.

---

## At a Glance

| ID | Change ID | Outcome | Prerequisites | Status |
| :--- | :--- | :--- | :--- | :--- |
| **F-01** | app-shell-and-routing | Router, AuthContext, Polish shell | — | ready |
| **F-02** | supabase-data-and-rls | Supabase schema, RLS, seeds | F-01 | proposed |
| **S-01** | owner-invitation-signup | Onboarding flow | F-01, F-02 | proposed |
| **S-02** | admin-verification | Verification queue | S-01 | proposed |
| **S-03** | profile-employee-invites | Company profile, invite system | S-02 | proposed |
| **S-04** | directory-search | Verified search (region/type/material) | S-03 | proposed |
| **S-05** | company-profile | Profile + employee list (no phone) | S-04 | proposed |
| **S-06** | **chat-phone-reveal** | 1:1 Chat + audited phone reveal | S-05 | proposed |
| **S-07** | pdf-attachments | PDF exchange (≤ 10 MB) | S-06 | proposed |
| **S-08** | realtime-badges | Realtime delivery, unread badges | S-06 | proposed |
| **S-09** | favorites-list | Starred companies | S-05 | proposed |
| **S-10** | employee-deactivation | History retention for Owner | S-03, S-06 | proposed |
| **S-11** | polymer-proposal | Admin-approved polymer catalog | S-02 | proposed |
| **S-12** | platform-lockout | Admin-level security controls | S-02 | proposed |

---

## Streams

| Stream | Theme | Chain |
| :--- | :--- | :--- |
| **A** | Onboarding & Verification | `F-01` → `F-02` → `S-01` → `S-02` → `S-03` |
| **B** | Discovery + North Star | `S-04` → `S-05` → `S-06` → `S-07` |
| **C** | Interactivity | `S-08` → `S-09` |
| **D** | Lifecycle & Moat | `S-10` → `S-12` |
| **E** | Catalog Growth | `S-11` |

---

## Baseline (as of 2026-05-26)

- **Frontend:** Partial (React 19, Vite 8, no router/UI).
- **Backend/API:** Absent (Supabase client available, but unused).
- **Data:** Absent (no schema/seeds).
- **Auth:** Absent.
- **Deploy/Infra:** Present (Cloudflare Pages, GitHub Actions, Husky).
- **Observability:** Absent.

---

## Backlog Handoff

| ID | Change ID | Ready for `/10x-plan` |
| :--- | :--- | :--- |
| F-01 | app-shell-and-routing | **yes** |
| F-02 | supabase-data-and-rls-baseline | no |
| S-01 | owner-invitation-and-signup | no |
| ... | (see full roadmap for details) | - |

---

## Parked
- Marketplace / classifieds board.
- Group chat (multi-party).
- In-platform payments.
- Native mobile app.
- Public sign-up.
- Voice / video calls.
- Image attachments.
- Public, unlogged-in company profiles.

---

## Open Roadmap Questions
1. **Scale:** MVP `medium` (≤100 firms). Ceiling: low thousands.
2. **Limits:** PDF > 10 MB (monitor feedback).
3. **Features:** Read-receipt toggle (if users complain).
4. **Fallback:** Email notifications (restore if active < 60%).
5. **Precision:** City-level search (if logistics require).