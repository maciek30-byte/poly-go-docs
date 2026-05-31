---
flow_id: UF-03
title: Adding employees
actor: Company Owner (Admin user)
trigger: Admin user navigates to the Employees tab in "My Company"
outcome: New employee profile created; employee receives email confirmation with login details
related_fr: FR-008, FR-009
---

# UF-03 — Adding employees

## Steps

1. Admin user presses the **"Menu"** button on the main dashboard.
2. Admin user presses **"My Company"**.
3. The "My Company" window opens.
4. Admin user presses the **"Employees"** tab header.
5. The "Employees" table with a list of current employees is displayed.
6. Admin user presses the **"Add Employee"** button.
7. The input fields panel / window appears.

### Section 1 — Personal details

8. Admin user fills in employee personal details and presses **"Next"**.

   **Required fields:**
   - User Name
   - Password
   - First Name
   - Last Name
   - Phone Number
   - Email Address
   - Job Title
   - Department
   - Location

   - **[VALIDATION]** All required fields filled?
     - NO → Display error: *"All required fields must be filled"* → Return to step 8.
   - **[VALIDATION]** Is the employee's name unique (no duplicate within company)?
     - NO → Display error: *"An employee with this name already exists"* → Return to step 8.
   - **[VALIDATION]** All fields with properly formatted data?
     - NO → Display error: *"Invalid data format"* → Return to step 8.
     - YES → Continue.

### Section 2 — Account settings

9. Admin user is redirected to the **Employee Account Settings** form (checkbox input).
10. Admin user selects appropriate options and presses **"Next"**.

    **Settings:**
    - **Roles** — assign role(s) to the employee
    - **Visibility** — set how this employee appears to other users

    - **[VALIDATION]** All required options selected?
      - NO → Display error: *"Select the appropriate options"* → Return to step 10.
      - YES → Continue.

### Section 3 — Profile photo

11. Admin user is redirected to the **"Add photo"** section.
12. Admin user decides to add a photo **or** skips this step, then presses **"Next"**.
    - **[VALIDATION]** (if photo added) File within correct size limit?
      - NO → Display error: *"File is too big"* → Return to step 12.
    - **[VALIDATION]** (if photo added) File has correct extension?
      - NO → Display error: *"Unallowed file extension"* → Return to step 12.
      - YES → Continue.

### Section 4 — Summary & save

13. Admin user is redirected to the **Summary** view.
14. Admin user verifies all data.
    - **Does the admin want to make changes?**
      - YES → Admin presses **"Go back"** → Returns to relevant section.
    - **Does the admin want to cancel?**
      - YES → Admin presses **"Cancel"**.
        - **Are you sure you want to cancel?**
          - YES → Changes discarded.
          - NO → Return to summary.
15. Admin user presses **"Save profile"**.
    - **[VALIDATION]** Success?
      - NO → Display error: *"Something went wrong"* → END.
      - YES → Display confirmation: *"Profile created successfully"*.
16. **[SYSTEM]** Added employee receives **email confirmation** with login details.
17. **END**

## Notes

- Only the Company Owner (Admin) can add employees — employees cannot self-register or invite others (FR-008).
- Open questions logged by Maciek: Can there be more than one Admin? (YES). Can an employee later change their own data without admin involvement? (TBD).
- The first user registered for the company is automatically assigned Admin role; this can be transferred to another user later.
