---
flow_id: UF-02
title: Company profile setup
actor: Company Owner (Admin user)
trigger: Admin user navigates to "My Company" after initial registration
outcome: Complete company profile created and saved; profile visible to other verified users per chosen visibility setting
related_fr: FR-003, FR-006, FR-007, FR-007a
---

# UF-02 — Company profile setup

## Steps

1. Admin user presses the **"Menu"** button on the main dashboard.
2. Admin user presses **"My Company"**.
3. The "My Company" window opens.
4. Admin user presses the **"Create company profile"** button.
5. The "Company profile" tab is displayed.

### Section 1 — Company & contact details

6. Admin user presses the **"Company profile"** tab header.
7. The input fields panel appears.
8. Admin user fills in **company details**, verifies pre-filled data from the registration process, and presses **"Next"**.

   **Required fields — Registration data:**
   - Company name
   - NIP / VAT ID
   - Street, ZIP code, Town, Country

   **Required fields — General contact (office / secretariat):**
   - Phone, Email, Website

   **Required fields — Personal contact:**
   - First & last name, Job title, Phone, Email, Website

   **Optional — Operational address (if different from registered address):**
   - Checkbox: *"Do you want to enter a different operational address?"*
   - If checked: Branch / division name (optional), Street, ZIP, Town, Country, contact details (phone, email, website, personal contact)

   - **[VALIDATION]** All required fields filled?
     - NO → Display error: *"All required fields must be filled"* → Return to step 8.
   - **[VALIDATION]** All fields with properly formatted data?
     - NO → Display error: *"Invalid data format"* → Return to step 8.
     - YES → Continue.

### Section 2 — Business profile

9. Admin user is redirected to the **Business Profile** form.
10. Admin user selects **Types of Activity** (multiple choice) and presses **"Next"**.

    Activity options:
    - Producer
    - Virgin materials supplier
    - Recycler
    - Waste management
    - Machinery and equipment supplier
    - Components and spare parts supplier
    - Technology / IT supplier
    - Trader
    - Other

    - **[VALIDATION]** All required options selected?
      - NO → Display error: *"All required fields must be selected"* → Return to step 10.
      - YES → Continue.

11. Admin user selects **main types of polymers** handled by the company from the curated catalog list and presses **"Next"**.
    - Admin user may also propose a new polymer not on the list (pending Platform Administrator approval — see FR-007a).

12. Admin user adds **company description** (optional, suggested structure: history / current activity / mission & vision) and presses **"Next"**.

### Section 3 — Attachments

13. Admin user is redirected to the **"Add logo", "Add photos", "Add files"** section.
14. Admin user adds:
    - **Logo** (drag & drop or file picker)
    - **Company photos** (drag & drop or file picker)
    - **PDF documents** (drag & drop or file picker)
15. Admin user presses **"Next"**.

    - **[VALIDATION]** All files within correct size limit?
      - NO → Display error: *"Files are too big"* → Return to step 14.
    - **[VALIDATION]** All files with allowed extensions?
      - NO → Display error: *"Unallowed file extensions"* → Return to step 14.
      - YES → Continue.

### Section 4 — Visibility settings

16. Admin user is redirected to the **Visibility** checkbox form.
17. Admin user selects visibility setting and presses **"Next"**.

    **Full visibility:**
    - All users can see full company info (data, addresses, contact details).
    - All users can contact any company employee via the messenger.

    **No visibility:**
    - Other users cannot see registration data, addresses, or contact details.
    - Visible to others: company name, logo, description, photos.
    - Other users cannot contact employees via the messenger.
    - Company's own employees can still view other companies and contact them via messenger.
    - Other users may send an **Invitation** to the company; invitation can include a **referral code** obtained from another platform user.

    - **[VALIDATION]** Decision made?
      - NO → Display error: *"You have to decide how other users will see your company"* → Return to step 17.
      - YES → Continue.

### Section 5 — Summary & save

18. Admin user is redirected to the **Summary** view.
19. Admin user verifies all data.
    - **Does the admin want to make changes?**
      - YES → Admin presses **"Go back"** → Returns to relevant section.
    - **Does the admin want to cancel?**
      - YES → Admin presses **"Cancel"** → Changes discarded.
      - NO → Continue.
20. Admin user presses **"Save profile"**.
    - **[VALIDATION]** Success?
      - NO → Display error: *"Something went wrong"* → END.
      - YES → Display confirmation: *"Profile created successfully"*.
21. **END**

## Notes

- Visibility setting can be changed at any time from within the platform.
- Editing NIP or KRS after activation resets the company back to `pending` state and triggers re-verification (FR-006).
- The polymer catalog is curated; newly proposed polymers are visible only on the proposer's profile until approved by the Platform Administrator (FR-007a).
