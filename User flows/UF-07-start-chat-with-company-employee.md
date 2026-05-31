---
flow_id: UF-07
title: Start a chat with a public company employee
actor: Employee
trigger: Employee wants to contact an employee from another verified company
outcome: Instant Messenger window opens; conversation can begin
related_fr: FR-010, FR-010a, FR-014, FR-015, FR-016
---

# UF-07 — Start a chat with a public company employee

## Steps

1. User (Employee) is on the **main dashboard**.
2. User presses the **"Menu"** button.
3. Sidenav "Menu" opens.
   - Note: The sidenav can be pinned open or hidden — the user controls this depending on screen size and preference.
4. User presses the **"Companies"** button.
5. The "Companies" list window opens.
6. User browses the list of verified companies and clicks on the **name of the selected company**.
7. The **"Company profile"** tab is displayed.
8. User presses the **"Employees"** tab header within the company profile.
9. The **"Employees"** table / list appears showing employees of that company.

   **Visible in list view (per FR-010):**
   - First name
   - Last name
   - Job title
   - Phone number is **NOT** shown at this stage.

10. User finds the person they want to contact and clicks the **"Instant Messenger" icon** next to the employee's name.
11. The **Instant Messenger window pops up**.
    - **[SYSTEM]** If this is the first message to this counterparty employee: a new persistent thread is created.
    - **[SYSTEM]** If a thread already exists: the existing thread is re-opened (no duplicate threads).
    - **[SYSTEM]** The counterparty's **phone number becomes visible** to the user in the chat view (FR-010a). This phone-reveal event is logged for anti-harvest audit.
12. User conducts the conversation using chat functionality.
13. **END**

## Notes

- Only employees of **activated** companies appear in the directory and company profile views (FR-013). Users never see pending, rejected, or locked companies.
- A second click on the same employee always re-opens the existing thread — never creates a duplicate (FR-014).
- Within the chat, the user can send text messages (FR-015) and attach PDF files up to 10 MB (FR-016).
- Browser push notification is sent to the counterparty if they are not currently active on the polyGo tab (FR-019).
