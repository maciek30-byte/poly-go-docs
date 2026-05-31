---
flow_id: UF-01
title: Company registration via invitation
actor: Prospective Company Owner
trigger: User receives an invitation email with a unique sign-up URL
outcome: Company created, admin user created, verification link sent to user email
related_fr: FR-001, FR-002, FR-003
---

# UF-01 — Company registration via invitation

## Steps

1. User clicks on the invitation URL.
2. User is redirected to the Invitation Page with a prefilled Invitation Code.
3. User presses the **"Create Company"** button.
   - **[VALIDATION]** Invitation code valid?
     - NO → Display error: *"Invitation code invalid"* → END (user cannot proceed).
     - YES → Continue.
4. User is redirected to a form with **company details**.
5. User fills in company data and presses **"Next"**.
   - **[VALIDATION]** All fields filled?
     - NO → Display error: *"All fields are required"* → Return to step 5.
     - YES → Continue.
   - **[VALIDATION]** All fields filled with properly formatted data?
     - NO → Display error: *"Invalid data format"* → Return to step 5.
     - YES → Continue.
6. User is redirected to a form with **admin (Company Owner) personal details**.
7. User fills in admin data and presses **"Next"**.
   - **[VALIDATION]** All fields filled?
     - NO → Display error: *"All fields are required"* → Return to step 7.
     - YES → Continue.
8. System checks: **User email already registered?**
   - YES → Display error: *"User already exists"* → END.
   - NO → System creates the user account.
9. **[SYSTEM]** Company is created with the new user assigned as Admin (Company Owner).
10. **[SYSTEM]** Verification link is sent to the user's email address.
    - **[VALIDATION]** Success?
      - NO → Display error: *"Something went wrong"* → END.
      - YES → Display confirmation: *"Profile created successfully"*.
11. **END**

## Notes

- The first user registered for a company automatically receives **Administrator (Company Owner)** permissions. This can be changed later in account settings.
- Sign-up is **invitation-only** — there is no public registration form (FR-001).
- After successful registration, the company enters `pending` state and awaits manual verification by the Platform Administrator (see UF-02).
