---
flow_id: UF-04
title: Editing employees
actor: Company Owner (Admin user)
trigger: Admin user navigates to a specific employee's profile in the Employees tab
outcome: Employee profile updated and saved; changes reflected immediately
related_fr: FR-008, FR-009
---

# UF-04 — Editing employees

## Entry point: Access employee management panel

1. Admin user presses the **"Menu"** button on the main dashboard.
2. Admin user presses **"My Company"**.
3. The "My Company" window opens.
4. Admin user presses the **"Employees"** tab header.
5. The "Employees" table with a list of current employees is displayed.
6. Admin user presses the **name** of the employee they want to edit.
7. An information panel / window with summarised employee details appears.
8. Admin user presses the **"Manage employee"** button.
9. The employee data editing panel / window appears.

---

## Branch A — Edit personal details

10a. Admin user presses the **"Employee details"** tab header.
11a. The **"Personal data"** tab with input fields is displayed.

    **Editable fields:**
    - User Name
    - Password
    - First Name
    - Last Name
    - Phone Number
    - Email Address
    - Job Title
    - Department
    - Location
    - Profile photo

12a. Admin user makes the required changes and presses **"Save"**.

    - **[VALIDATION]** All required fields filled?
      - NO → Display error: *"All required fields must be filled"* → Return to step 12a.
    - **[VALIDATION]** Are required options selected?
      - NO → Display error: *"Select the appropriate options"* → Return to step 12a.
    - **[VALIDATION]** (if photo changed) Is the photo file within correct size?
      - NO → Display error: *"File is too big"* → Return to step 12a.
    - **[VALIDATION]** (if photo changed) Does the photo file have the correct extension?
      - NO → Display error: *"Unallowed file extension"* → Return to step 12a.
      - YES → Continue.

    - **[VALIDATION]** Success?
      - NO → Display error: *"Something went wrong"* → END.
      - YES → Display confirmation: *"Changes saved successfully"*.

13a. Information panel / window with summarised employee details appears.
14a. Admin user presses **"Close"**.
15a. Returns to "Employees" table.
16a. **END**

---

## Branch B — Edit account settings

10b. Admin user presses the **"Account Settings"** tab header.
11b. The **"Account Settings"** tab with checkboxes is displayed.

    **Editable settings:**
    - Roles
    - Visibility

12b. Admin user makes the required changes and presses **"Save"**.

    - **[VALIDATION]** Are required options selected?
      - NO → Display error: *"Select the appropriate options"* → Return to step 12b.

    - **[VALIDATION]** Success?
      - NO → Display error: *"Something went wrong"* → END.
      - YES → Display confirmation: *"Changes saved successfully"*.

13b. Information panel / window with summarised employee details appears.
14b. Admin user presses **"Close"**.
15b. Returns to "Employees" table.
16b. **END**
