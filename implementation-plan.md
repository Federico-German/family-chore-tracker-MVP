### Implementation Plan

This plan outlines the steps to build the Family Chore Management App MVP based on the provided Product Requirements Document (PRD).

**Preamble:**
*   **Technology Stack:** This plan assumes a standard web stack (e.g., Frontend: React/Vue/Angular, Backend: Node.js/Python/Django/Ruby on Rails, Database: PostgreSQL/MySQL/MongoDB). Specific choices should be made before starting Phase 1.
*   **Git Commits:** After completing each step and verifying its tests, prompt the development assistant AI to create a Git commit. For example: "Create a Git commit for the completed work in Step 1.1: Initialized web project and database setup."

--- 

**Phase 1: Project Setup & Core User/Family Management**

*   **Goal:** Establish the project foundation, database, user authentication, and basic family structure.

    **Step 1.1: Initialize Web Project & Database Setup**
    *   **Tasks:**
        1.  Choose and set up the frontend framework (e.g., Create React App, Vue CLI).
        2.  Choose and set up the backend framework (e.g., Express.js, Django).
        3.  Choose, install, and configure the database (e.g., PostgreSQL, MongoDB).
        4.  Establish basic project structure, version control (Git), and environment configuration.
    *   **Manual Tests:**
        1.  Verify that the frontend development server can run and serve a placeholder page.
        2.  Verify that the backend server can run and respond to a simple test API endpoint.
        3.  Confirm that the application can connect to the database.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 1.1: Initialized web project and database setup."

    **Step 1.2: Implement `Family` and `User` Data Models**
    *   **Tasks:**
        1.  Define and implement the `Family` model schema as per PRD Section 5:
            *   `FamilyID` (PK)
            *   `FamilyName`
            *   `AccountCreatorUserID` (FK to User)
        2.  Define and implement the `User` model schema as per PRD Section 5:
            *   `UserID` (PK)
            *   `FamilyID` (FK to Family)
            *   `Name` / `Username` (e.g., display name)
            *   `Email` (unique, for login)
            *   `PasswordHash`
    *   **Manual Tests:**
        1.  Using database tools or a test script, confirm that records can be created, read, updated, and deleted for both `Family` and `User` tables/collections.
        2.  Verify that relationships (e.g., `FamilyID` in `User`) are correctly established.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 1.2: Implemented Family and User data models."

    **Step 1.3: Implement User Registration (Email/Password) & Account Creation (Implicit Family Creation)**
    *   **Tasks:**
        1.  Create a registration UI (form for email, password, name).
        2.  Implement backend logic for user registration:
            *   Validate input (email format, password complexity if any).
            *   Check for existing email.
            *   Hash the password.
            *   Create a new `User` record.
            *   Automatically create a new `Family` record, setting the new user as `AccountCreatorUserID` and associating the user with this family.
            *   Log the user in upon successful registration.
    *   **Manual Tests:**
        1.  Navigate to the registration page.
        2.  Attempt to register with an invalid email format; verify error message.
        3.  Attempt to register with a valid email and password.
        4.  Verify a new `User` record is created in the database with a hashed password.
        5.  Verify a new `Family` record is created, linked to the new user.
        6.  Verify the user is redirected to a logged-in area (e.g., a placeholder dashboard).
        7.  Attempt to register again with the same email; verify error message.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 1.3: Implemented user registration and initial family creation."

    **Step 1.4: Implement User Login & Session Management**
    *   **Tasks:**
        1.  Create a login UI (form for email, password).
        2.  Implement backend logic for user login:
            *   Validate input.
            *   Find user by email.
            *   Verify hashed password.
            *   Establish a session (e.g., using JWTs or server-side sessions).
        3.  Implement logout functionality.
        4.  Protect routes/endpoints that require authentication.
    *   **Manual Tests:**
        1.  Navigate to the login page.
        2.  Attempt to log in with incorrect credentials; verify error message.
        3.  Log in with correct credentials; verify successful login and redirection.
        4.  Attempt to access a protected page without logging in; verify redirection to login.
        5.  Access a protected page after logging in; verify access is granted.
        6.  Log out; verify session is terminated and access to protected pages is revoked.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 1.4: Implemented user login, logout, and session management."

    **Step 1.5: Implement Family Member Management (Admin Functionality - Adding Members)**
    *   **Tasks:**
        1.  Create a basic UI section accessible only to the Account Creator (Admin) for adding family members (PRD 3.1.3, 4.2.3).
        2.  Backend logic for Admin to add a new `User` to their `Family`:
            *   Input: Name, Email, initial Password for the new member.
            *   The new `User` record should be associated with the Admin's `FamilyID`.
    *   **Manual Tests:**
        1.  Log in as the Account Creator (Admin).
        2.  Navigate to the family management section.
        3.  Add a new family member with a name, email, and initial password.
        4.  Verify the new `User` record is created in the database, linked to the correct `FamilyID`.
        5.  Log out as Admin. Log in as the newly added family member using their email and initial password.
        6.  Attempt to access the family management section as the new non-admin member; verify access is denied.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 1.5: Implemented admin functionality for adding family members."

--- 

**Phase 2: Chore Definition & Basic Lifecycle**

*   **Goal:** Implement the creation, display, claiming, and completion of chores.

    **Step 2.1: Implement `Chore` Data Model**
    *   **Tasks:**
        1.  Define and implement the `Chore` model schema as per PRD Section 5:
            *   `ChoreID` (PK)
            *   `FamilyID` (FK)
            *   `Name` (Text, not null)
            *   `Description` (Text, nullable)
            *   `DueDate` (Date, nullable)
            *   `RecurrenceRule` (Text, e.g., 'none', 'daily', 'weekly', nullable)
            *   `Status` (Text, e.g., 'available', 'in_progress', 'completed', default: 'available')
            *   `CreatedByUserID` (FK to User)
            *   `AssignedToUserID` (FK to User, nullable)
            *   `LastInstanceDate` (Date, nullable - for recurring chores)
    *   **Manual Tests:**
        1.  Using database tools or a test script, confirm records can be created, read, updated, and deleted for the `Chore` table/collection.
        2.  Verify all fields, including defaults and nullability constraints.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 2.1: Implemented Chore data model."

    **Step 2.2: Implement Chore Creation Functionality (UI & Backend)**
    *   **Tasks:**
        1.  Create a UI form for creating chores (PRD 3.2.2): Name, Description, Due Date, Recurrence.
        2.  Implement backend logic for any logged-in family member to create a chore:
            *   Validate input.
            *   Associate the chore with the creator's `FamilyID` and `UserID` (`CreatedByUserID`).
            *   Set initial `Status` to 'available'.
            *   If it's a non-recurring chore with a due date, `LastInstanceDate` can be the `DueDate` or null. If recurring, `LastInstanceDate` should be set to the first occurrence's date.
    *   **Manual Tests:**
        1.  Log in as any family member.
        2.  Navigate to the chore creation UI.
        3.  Create a chore with all fields filled (including due date and a recurrence like 'daily').
        4.  Verify the chore is saved to the database with correct `FamilyID`, `CreatedByUserID`, `Status` ('available'), and other attributes.
        5.  Create a chore with only the required field (Name) and no recurrence.
        6.  Verify this chore is also saved correctly.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 2.2: Implemented chore creation functionality."

    **Step 2.3: Implement Chore Listing (Basic View)**
    *   **Tasks:**
        1.  Create a UI to display a list of all chores belonging to the logged-in user's family.
        2.  For each chore, display at least: Name, Status, Due Date (if any).
        3.  Initially, show all chores regardless of status.
    *   **Manual Tests:**
        1.  Log in as a family member.
        2.  Create several chores.
        3.  Navigate to the chore list view.
        4.  Verify all created chores for the family are displayed with their name, status, and due date.
        5.  Log in as a member of a different family (if test data allows, otherwise conceptually verify filtering by `FamilyID`). Verify they only see their family's chores.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 2.3: Implemented basic chore listing for the family."

    **Step 2.4: Implement Chore Claiming ("Picking") Functionality**
    *   **Tasks:**
        1.  In the chore list, add a 'Pick Chore' button/action for chores with 'available' status.
        2.  Implement backend logic: When a user picks a chore:
            *   Update the chore's `Status` to 'in_progress' (or 'taken').
            *   Set `AssignedToUserID` to the ID of the user who picked it.
            *   Ensure only one user can pick an available chore (first-come, first-served).
        3.  The 'Pick Chore' button should not be visible or should be disabled for chores that are not 'available'.
    *   **Manual Tests:**
        1.  Log in. View the list of available chores.
        2.  Click 'Pick Chore' for an available chore.
        3.  Verify the chore's status changes to 'in_progress' in the UI and database.
        4.  Verify `AssignedToUserID` is set to the current user in the database.
        5.  Verify the 'Pick Chore' button is no longer available for this chore.
        6.  (Optional, if concurrent testing is possible) Have another user try to pick the same chore simultaneously or immediately after; verify only the first user succeeds.
        7.  Log in as another user in the same family. Verify they see the chore as 'in_progress' and cannot pick it.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 2.4: Implemented chore claiming (picking) functionality."

    **Step 2.5: Implement Chore Completion Functionality (Self-verified)**
    *   **Tasks:**
        1.  For chores that are 'in_progress' and assigned to the current user, add a 'Mark as Complete' button/action.
        2.  Implement backend logic: When a user marks a chore as complete:
            *   Update the chore's `Status` to 'completed'.
            *   (Point calculation will be added in Phase 3).
        3.  The 'Mark as Complete' button should only be visible/enabled for the `AssignedToUserID`.
    *   **Manual Tests:**
        1.  Log in as the user who picked a chore ('User A').
        2.  View the chore they picked (status 'in_progress').
        3.  Click 'Mark as Complete'.
        4.  Verify the chore's status changes to 'completed' in the UI and database.
        5.  Log in as another user ('User B'). View the same chore. Verify they cannot mark it as complete if it was assigned to 'User A'.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 2.5: Implemented chore completion functionality (self-verified)."

--- 

**Phase 3: Personal Value System & Point Calculation**

*   **Goal:** Implement the personal value assignment for chores and the calculation of points upon completion.

    **Step 3.1: Implement `UserChoreValue` Data Model**
    *   **Tasks:**
        1.  Define and implement the `UserChoreValue` model schema as per PRD Section 5:
            *   `UserChoreValueID` (PK)
            *   `UserID` (FK to User)
            *   `ChoreID` (FK to Chore)
            *   `PersonalValue` (Integer, 1-10)
            *   Unique constraint on (`UserID`, `ChoreID`).
    *   **Manual Tests:**
        1.  Using database tools or a test script, confirm records can be created, read, updated, and deleted for `UserChoreValue`.
        2.  Verify the unique constraint: attempt to add two values for the same user and chore; the second attempt should fail.
        3.  Verify `PersonalValue` accepts integers between 1 and 10.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 3.1: Implemented UserChoreValue data model."

    **Step 3.2: Implement Personal Value Assignment UI & Logic**
    *   **Tasks:**
        1.  In the chore detail view (or alongside each chore in a list), allow users to see and set/update their `PersonalValue` (1-10 scale) for any chore in their family (PRD 3.3.3).
        2.  Backend logic to save/update the `UserChoreValue` for the logged-in user and the specific chore.
    *   **Manual Tests:**
        1.  Log in. View a chore.
        2.  Assign a personal value (e.g., 7) to the chore.
        3.  Verify the value is saved in the `UserChoreValue` table for the current user and this chore.
        4.  Change the personal value for the same chore (e.g., to 3).
        5.  Verify the `UserChoreValue` record is updated.
        6.  Log in as a different family member. Assign their own personal value to the same chore.
        7.  Verify a new `UserChoreValue` record is created for this second user, and the first user's value remains unchanged.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 3.2: Implemented personal value assignment for chores."

    **Step 3.3: Implement `ChoreCompletion` Data Model**
    *   **Tasks:**
        1.  Define and implement the `ChoreCompletion` model schema as per PRD Section 5:
            *   `CompletionID` (PK)
            *   `ChoreID` (FK to Chore)
            *   `CompletedByUserID` (FK to User)
            *   `CompletionDate` (Timestamp, default to now)
            *   `PointsAwarded` (Numeric)
    *   **Manual Tests:**
        1.  Using database tools or a test script, confirm records can be created, read, updated, and deleted for `ChoreCompletion`.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 3.3: Implemented ChoreCompletion data model."

    **Step 3.4: Implement Value Point Calculation Logic & Storing on Completion**
    *   **Tasks:**
        1.  Modify the chore completion logic (from Step 2.5):
            *   When a chore is marked complete by `CompletedByUserID`:
                *   Fetch all `UserChoreValue.PersonalValue` entries for that `ChoreID` *excluding* the value from `CompletedByUserID`.
                *   Calculate the average of these collected personal values.
                *   **Edge Case Handling (PRD 3.3):** If no other family members have assigned a value, `PointsAwarded` will be 0 for MVP.
                *   Create a new `ChoreCompletion` record storing `ChoreID`, `CompletedByUserID`, `CompletionDate`, and the calculated `PointsAwarded`.
    *   **Manual Tests:**
        1.  Setup: Family with User A, User B, User C. Chore X exists.
        2.  User A assigns value 2 to Chore X.
        3.  User B assigns value 8 to Chore X.
        4.  User C assigns value 5 to Chore X.
        5.  User A picks and completes Chore X.
        6.  Verify a `ChoreCompletion` record is created for User A and Chore X.
        7.  Verify `PointsAwarded` for User A is (8+5)/2 = 6.5.
        8.  Setup: Chore Y. Only User A assigns value 10. No other users assign values.
        9.  User A picks and completes Chore Y.
        10. Verify `PointsAwarded` for User A is 0.
        11. Setup: Chore Z. User A assigns 1, User B assigns 9. User C completes Chore Z (without assigning a value themselves).
        12. Verify `PointsAwarded` for User C is (1+9)/2 = 5.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 3.4: Implemented value point calculation and storage on chore completion."

--- 

**Phase 4: UI Views & Core Features Integration**

*   **Goal:** Develop the main UI views (Dashboard, Chore Management, Profile) and integrate core functionalities like filtering and recurring chores.

    **Step 4.1: Develop Chore Management Page (with Filtering)**
    *   **Tasks:**
        1.  Create/Refine the dedicated Chore Management Page (PRD 4.2.2).
        2.  Display the list of chores with details (Name, Description, Due Date, Status, Assigned To, Created By).
        3.  Implement filtering capabilities (PRD 3.2.4):
            *   By `Status` ('Available', 'In Progress', 'Completed').
            *   By `Relevance to User` (e.g., 'Picked by me', 'Created by me').
        4.  Ensure actions like 'Pick Chore', 'Mark as Complete', 'Assign Personal Value', and 'Create Chore' are accessible from this page.
        5.  Allow users to edit/delete chores they created (if chore is not 'in_progress' by someone else or 'completed').
    *   **Manual Tests:**
        1.  Navigate to the Chore Management Page.
        2.  Verify all chores for the family are listed by default.
        3.  Test filter by 'Available': only available chores show.
        4.  Test filter by 'In Progress': only in-progress chores show.
        5.  Test filter by 'Completed': only completed chores show.
        6.  Test filter 'Picked by me': only chores picked by the current user show.
        7.  Test filter 'Created by me': only chores created by the current user show.
        8.  Combine filters if applicable (e.g., 'Picked by me' AND 'In Progress').
        9.  Verify chore creation, picking, completion, and value assignment can be initiated from this page.
        10. Create a chore. Edit its name/description. Delete it (if not picked/completed).
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 4.1: Developed Chore Management Page with advanced listing and filtering."

    **Step 4.2: Develop Personal Profile Page**
    *   **Tasks:**
        1.  Create a Personal Profile Page for each family member (PRD 4.2.4).
        2.  Display the logged-in user's performance statistics (PRD 3.4):
            *   Total number of tasks completed (count of `ChoreCompletion` records for the user).
            *   Cumulative 'value points' earned (sum of `PointsAwarded` from `ChoreCompletion` records for the user).
    *   **Manual Tests:**
        1.  Log in as User A, who has completed 2 chores for 5 and 10 points respectively.
        2.  Navigate to User A's Personal Profile Page.
        3.  Verify 'Total tasks completed' shows 2.
        4.  Verify 'Cumulative value points earned' shows 15.
        5.  Log in as User B, who has completed 0 chores.
        6.  Navigate to User B's Personal Profile Page.
        7.  Verify 'Total tasks completed' shows 0 and 'Cumulative value points earned' shows 0.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 4.2: Developed Personal Profile Page with performance statistics."

    **Step 4.3: Develop Dashboard View**
    *   **Tasks:**
        1.  Create the Dashboard page (PRD 4.2.1).
        2.  Display a list/summary of 'Available' chores.
        3.  Display a summary of the logged-in user's personal statistics (can link to Profile Page).
        4.  (Basic) Display a feed of recent family activity (e.g., "[User X] completed [Chore Y]", "[User Z] created [Chore W]"). Limit to last 5-10 activities.
    *   **Manual Tests:**
        1.  Log in. Navigate to the Dashboard.
        2.  Verify a list of 'Available' chores is visible.
        3.  Verify the personal stats summary (tasks completed, points) for the logged-in user is shown.
        4.  Perform some actions (create a chore, complete a chore by another family member). Refresh dashboard.
        5.  Verify the recent activity feed updates accordingly (if implemented).
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 4.3: Developed Dashboard view with key summaries."

    **Step 4.4: Implement Basic Recurring Chore Logic**
    *   **Tasks:**
        1.  When a chore with a `RecurrenceRule` (e.g., 'daily', 'weekly') is marked 'completed':
            *   Keep the original chore instance as 'completed'.
            *   Create a *new* `Chore` record (a new instance of the recurring chore).
            *   The new chore should have the same Name, Description, RecurrenceRule, FamilyID, CreatedByUserID.
            *   Its `Status` should be 'available'.
            *   `AssignedToUserID` should be null.
            *   Calculate and set the new `DueDate` and `LastInstanceDate` based on the `RecurrenceRule` and the completed instance's `DueDate` or `CompletionDate`.
                *   Example: If 'daily' and completed on Monday, new DueDate is Tuesday.
                *   Example: If 'weekly' on Monday and completed, new DueDate is next Monday.
    *   **Manual Tests:**
        1.  Create a chore with `Name`: "Daily Task", `RecurrenceRule`: 'daily', `DueDate`: Today.
        2.  Pick and complete this "Daily Task".
        3.  Verify the original chore instance is marked 'completed'.
        4.  Verify a *new* chore instance named "Daily Task" is created with `Status`: 'available', `DueDate`: Tomorrow, and the same recurrence rule.
        5.  Create a chore with `Name`: "Weekly Task", `RecurrenceRule`: 'weekly', `DueDate`: This Monday.
        6.  Pick and complete this "Weekly Task" on Wednesday.
        7.  Verify the original is 'completed'.
        8.  Verify a new "Weekly Task" is created with `Status`: 'available', `DueDate`: Next Monday.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 4.4: Implemented basic recurring chore regeneration on completion."

--- 

**Phase 5: Final Touches & MVP Polish**

*   **Goal:** Refine the application with admin tools, validation, UI polish, and thorough testing.

    **Step 5.1: Enhance Family Management Section (Admin UI)**
    *   **Tasks:**
        1.  Expand the Family Management Section for the Admin (PRD 4.2.3).
        2.  In addition to adding members (Step 1.5), allow Admin to:
            *   View a list of all family members.
            *   Edit basic profile information of members (e.g., Name). (Password changes might be out of scope for admin, self-service is better).
            *   Remove family members from the family (consider implications, e.g., what happens to their completed chores - for MVP, they remain, but user is deactivated or disassociated).
    *   **Manual Tests:**
        1.  Log in as Admin.
        2.  Navigate to Family Management.
        3.  Verify list of family members is displayed.
        4.  Edit the name of a family member. Verify change is saved and displayed.
        5.  Remove a family member. Verify they are removed from the list and can no longer log in (or are marked inactive).
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 5.1: Enhanced Family Management section for Admin."

    **Step 5.2: Input Validation and Error Handling**
    *   **Tasks:**
        1.  Review all user input forms (registration, login, chore creation, value assignment, etc.).
        2.  Implement comprehensive frontend and backend validation (e.g., required fields, data types, length limits, numerical ranges for values).
        3.  Provide clear, user-friendly error messages for validation failures.
        4.  Implement global error handling for unexpected server errors (e.g., display a generic error page or message).
    *   **Manual Tests:**
        1.  Attempt to submit forms with missing required fields; verify specific error messages.
        2.  Enter invalid data types (e.g., text in a date field if not using a date picker, value outside 1-10 for personal value); verify errors.
        3.  Test edge cases for inputs.
        4.  (If possible) Simulate a server error for an API call; verify a user-friendly error is shown instead of a crash or raw error data.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 5.2: Implemented comprehensive input validation and error handling."

    **Step 5.3: General UI/UX Review and Polish**
    *   **Tasks:**
        1.  Review the overall application flow and user experience.
        2.  Ensure consistent styling and layout across all pages.
        3.  Check for usability issues (e.g., clear navigation, intuitive controls).
        4.  Ensure responsiveness for common web browser sizes (desktop and mobile web as per PRD 4.1).
        5.  Strive for basic web accessibility (e.g., keyboard navigation, alt text for images if any, clear contrasts).
    *   **Manual Tests:**
        1.  Navigate through all app features on a desktop browser.
        2.  Navigate through all app features on a mobile browser (or responsive view in desktop developer tools).
        3.  Check for consistent look and feel.
        4.  Try to use the app using only the keyboard for navigation and interaction where appropriate.
        5.  Verify UI elements are clear and actions are predictable.
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 5.3: Completed general UI/UX review and polish."

    **Step 5.4: End-to-End Testing and Bug Fixing**
    *   **Tasks:**
        1.  Perform thorough end-to-end testing of all user stories and features defined in the PRD.
        2.  Create multiple user accounts representing a family, assign chores, values, complete chores, and check stats.
        3.  Test all edge cases identified during development.
        4.  Identify and fix any remaining bugs.
        5.  Prepare for MVP deployment.
    *   **Manual Tests:**
        1.  **Scenario 1 (Full Family Flow):**
            *   Admin registers, creates family.
            *   Admin adds 2 more family members.
            *   Member 1 logs in, creates 2 chores (1 one-time, 1 daily recurring).
            *   Member 2 logs in, creates 1 chore.
            *   All 3 members assign personal values (1-10) to all 3 chores.
            *   Member 1 picks and completes their one-time chore. Verify points awarded based on Member 2 & Admin's values. Verify stats update.
            *   Member 2 picks and completes Member 1's daily recurring chore. Verify points, stats, and that the daily chore regenerates for the next day.
            *   Admin picks and completes Member 2's chore. Verify points and stats.
            *   Check Dashboard for available chores (the regenerated daily chore).
            *   Check Chore Management page filters.
            *   Check Personal Profile pages for all 3 members for correct stats.
        2.  Test all error conditions and validation paths again.
        3.  Test user logout and session expiry (if applicable).
    *   **Git Commit Prompt:** After all tests for this step pass, prompt the development assistant AI: "Create a Git commit for the completed work in Step 5.4: Completed end-to-end testing and final bug fixes for MVP."

--- 

This implementation plan provides a structured approach to developing the Family Chore Management App MVP. Each step builds upon the previous ones, leading to a functional application meeting the specified requirements.