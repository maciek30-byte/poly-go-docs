---
flow_id: UF-06
title: Editing employee role
actor: Company Owner (Admin user)
trigger: Admin user navigates to an employee's Account Settings to change their role
outcome: Employee role updated; new permissions apply immediately
related_fr: FR-008
---

# UF-06 — Editing employee role

## Entry point: Access employee management panel

1. Admin user presses the **"Menu"** button on the main dashboard.
2. Admin user presses **"My Company"**.
3. The "My Company" window opens.
4. Admin user presses the **"Employees"** tab header.
5. The "Employees" table with a list of current employees is displayed.
6. Admin user presses the **name** of the employee whose role they want to change.
7. An information panel / window with summarised employee details appears.
8. Admin user presses the **"Manage employee"** button.
9. The employee data editing panel / window appears.

## Role change

10. Admin user presses the **"Account Settings"** tab header.
11. The **"Account Settings"** tab with checkboxes is displayed.

    **Settings:**
    - Roles
    - Visibility

12. Admin user makes the required changes to the **role setting** and presses **"Save"**.

    - **[VALIDATION]** Are the required options selected?
      - NO → Display error: *"Select the appropriate options"* → Return to step 12.
      - YES → Continue.

13. **[VALIDATION]** Success?
    - NO → Display error: *"Something went wrong"* → END.
    - YES → Display confirmation: *"Changes saved successfully"*.

14. Information panel / window with summarised employee details appears.
15. Admin user presses **"Close"**.
16. Returns to "Employees" table.
17. **END**

## Notes

- An Admin can transfer their own Admin permissions to another employee at any time.
- Multiple employees can hold Admin (Company Owner) role simultaneously.
- Role changes take effect immediately after saving.
