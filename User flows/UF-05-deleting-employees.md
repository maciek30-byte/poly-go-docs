---
flow_id: UF-05
title: Deleting employees
actor: Company Owner (Admin user)
trigger: Admin user navigates to a specific employee's profile in the Employees tab
outcome: Employee profile deleted; employee removed from the company's employee list
related_fr: FR-022
---

# UF-05 — Deleting employees

## Entry point: Access employee management panel

1. Admin user presses the **"Menu"** button on the main dashboard.
2. Admin user presses **"My Company"**.
3. The "My Company" window opens.
4. Admin user presses the **"Employees"** tab header.
5. The "Employees" table with a list of current employees is displayed.
6. Admin user presses the **name** of the employee they want to delete.
7. An information panel / window with summarised employee details appears.
8. Admin user presses the **"Manage employee"** button.
9. The employee data editing panel / window appears.

## Deletion

10. Admin user presses the **"Delete employee"** button.
11. Confirmation prompt: *"Are you sure you want to delete the employee?"*
    - Admin presses **"Cancel"** → Returns to employee editing panel. **END** (no change).
    - Admin presses **"Yes"** → Continue.

12. **[VALIDATION]** Success?
    - NO → Display error: *"Something went wrong"* → END.
    - YES → Display confirmation: *"Profile deleted"*.

13. Returns to "Employees" table with the deleted employee no longer listed.
14. **END**

## Notes

- Deletion is distinct from **deactivation** (FR-022). Deletion removes the employee record; deactivation blocks login while preserving chat history for the Company Owner (FR-023).
- Maciek to confirm: does "delete" in this flow mean permanent deletion or deactivation? Chat history retention rules (FR-023) may require this to be a deactivation, not a hard delete.
