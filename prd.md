# Product Requirements Document: Family Chore Management App (MVP)

## 1. Introduction

### 1.1. Product Overview
The Family Chore Management App is a web application designed to help families collaboratively manage household chores. It aims to foster fairness, motivation, and harmony by incorporating a unique personal value system that acknowledges individual preferences for tasks and tracks contributions. This document outlines the requirements for the Minimum Viable Product (MVP).

### 1.2. Goals
*   To provide a clear and organized system for tracking household chores.
*   To distribute chores more fairly by allowing members to account for personal dislike of tasks.
*   To motivate family members to participate in household tasks through a transparent value point system.
*   To reduce conflicts over chores by creating an objective record of contributions.
*   To offer flexibility in how chores are picked and completed within the family unit.

### 1.3. Target Audience
Families seeking an effective and engaging way to organize and distribute household responsibilities.

## 2. User Roles and Permissions

### 2.1. Family Member
*   Any registered family member can create chores.
*   Any registered family member can pick available chores to complete.
*   Family members can manage chores they have created (e.g., edit, delete).
*   Family members assign their personal value (dislike rating) to any chore.
*   Family members can view their own performance statistics.
*   Family members can mark chores they picked as completed.

### 2.2. Account Creator (Admin)
*   The user who creates the family account acts as the primary Admin.
*   The Admin is responsible for manually adding other family members to the family unit.
*   The Admin has all permissions of a regular Family Member.

## 3. Core Features

### 3.1. User Account and Family Management
*   **Authentication:** Users will register and log in using a standard email and password system.
*   **Family Unit Structure:** The application is designed for a single family unit per account. The account effectively represents the family.
*   **Adding Family Members:** The Admin (account creator) manually adds other family members to the unit (e.g., by creating profiles for them within the family account).

### 3.2. Chore Lifecycle Management
*   **Chore Creation:** Any family member can create a chore.
*   **Chore Attributes:** Each chore must include:
    *   `Chore Name`: A descriptive title for the task.
    *   `Description`: Optional additional details about the task.
    *   `Due Date`: Optional date by which the chore should be completed.
    *   `Recurrence`: Defines if the chore is one-time or recurring (e.g., none, daily, weekly).
*   **Chore Scheduling:** Both one-time and recurring chores are supported. Recurring chores will regenerate based on their schedule after completion or on a set interval.
*   **Chore Discovery and Display:**
    *   Chores are displayed in a primary list view.
    *   The list will be filterable by:
        *   `Status`: e.g., 'Available', 'In Progress' (taken), 'Completed'.
        *   `Relevance to User`: e.g., chores picked by the current user, chores created by the current user.
*   **Chore Claiming ("Picking")**:
    *   Chores are available on a first-come, first-served basis.
    *   When a family member picks a chore, its status changes to 'In Progress' (or 'Taken') and it is assigned to that member, making it unavailable for others.
*   **Chore Completion and Verification:**
    *   The family member who picked the chore marks it as completed.
    *   Completion is self-verified; no approval from other members is required for MVP.

### 3.3. Personal Value System & Points
*   **Individual Value Assignment:** Each family member can assign their own personal 'dislike' value to any chore within the family. This value is unique per user per chore.
*   **Value Representation:** The personal value is represented on a numerical scale from 1 to 10. A higher number indicates a greater dislike for the chore (e.g., 1 = "don't mind", 10 = "really hate").
*   **Timing of Value Assignment:** Users assign their personal value to a chore when viewing its details or when they first see it in a list. Users can update their personal value for any chore at any time.
*   **Value Point Calculation for Completed Chores:**
    *   When a family member completes a chore, they earn 'value points'.
    *   Points earned are calculated as the *average* of the personal values assigned to that specific chore by *all other* family members.
    *   *Edge Case Handling:* If no other family members (or an insufficient number) have assigned a value to a chore, a fallback mechanism for point calculation will be defined during development (e.g., points based on a default chore value, the chore creator's value if available, or zero points).

### 3.4. Performance Tracking (MVP)
*   **Individual Statistics:** The app will track and display for each family member:
    *   Total number of tasks completed.
    *   Cumulative 'value points' earned.

## 4. User Interface (Web Application)

### 4.1. Platform
*   The MVP will be a web application, accessible via standard desktop and mobile web browsers.

### 4.2. Key Screens / Views
*   **Dashboard:**
    *   A central overview page.
    *   Displays available chores.
    *   Shows a summary of the logged-in user's personal statistics (tasks completed, points earned).
    *   May include a feed of recent family activity (e.g., chores completed by others).
*   **Chore Management Page:**
    *   Comprehensive list of all chores with filtering capabilities (by status, relevance to user).
    *   Functionality to create new chores.
    *   Interface to view chore details and assign/update personal values.
    *   Options to manage chores (e.g., edit/delete chores created by the user, pick chores, mark chores as complete).
*   **Family Management Section:**
    *   Accessible by the Admin.
    *   Interface to add new family members to the unit.
    *   Interface to manage existing family members (e.g., edit profile information, remove from family).
*   **Personal Profile Page:**
    *   Dedicated page for each family member.
    *   Displays their detailed performance statistics: total tasks completed and cumulative value points.
    *   May allow users to manage their personal preferences or view their history of valued/completed chores.

## 5. Data Model (Core Entities)
*   **`User`**:
    *   `UserID` (Primary Key)
    *   `FamilyID` (Foreign Key)
    *   `Name` / `Username`
    *   `Email` (for login, unique)
    *   `PasswordHash`
    *   Other profile information (e.g., display name).
*   **`Family`**:
    *   `FamilyID` (Primary Key)
    *   `FamilyName`
    *   `AccountCreatorUserID` (Foreign Key to User, identifies Admin).
*   **`Chore`**:
    *   `ChoreID` (Primary Key)
    *   `FamilyID` (Foreign Key)
    *   `Name` (Text, not null)
    *   `Description` (Text, nullable)
    *   `DueDate` (Date, nullable)
    *   `RecurrenceRule` (Text, e.g., 'none', 'daily', 'weekly_monday', nullable)
    *   `Status` (Text, e.g., 'available', 'in_progress', 'completed')
    *   `CreatedByUserID` (Foreign Key to User)
    *   `AssignedToUserID` (Foreign Key to User, nullable - who picked it)
    *   `LastInstanceDate` (Date, for recurring chores to track current instance)
*   **`UserChoreValue`**: (Stores individual dislike ratings)
    *   `UserChoreValueID` (Primary Key)
    *   `UserID` (Foreign Key to User)
    *   `ChoreID` (Foreign Key to Chore)
    *   `PersonalValue` (Integer, 1-10)
    *   Unique constraint on (`UserID`, `ChoreID`)
*   **`ChoreCompletion`**: (Tracks completed chores and points earned)
    *   `CompletionID` (Primary Key)
    *   `ChoreID` (Foreign Key to Chore)
    *   `CompletedByUserID` (Foreign Key to User)
    *   `CompletionDate` (Timestamp)
    *   `PointsAwarded` (Numeric)

## 6. Non-Functional Requirements (for MVP)
*   **Usability:** The application must be intuitive and easy for family members of varying technical comfort levels to use.
*   **Performance:** Chore lists and updates should load reasonably quickly for typical family sizes and chore volumes.
*   **Reliability:** Core calculations (points) and state changes (chore status) must be accurate and dependable.
*   **Accessibility:** Strive for basic web accessibility standards (e.g., WCAG A/AA where feasible for MVP).

## 7. Future Considerations (Out of Scope for MVP)
The following features are potential enhancements for future versions:
*   Advanced performance tracking: charts, trends, contribution patterns over time.
*   Configurable reward systems tied to value points.
*   Notifications (in-app or email) for due dates, new chores, or completed chores.
*   Family leaderboards or achievement badges.
*   Integration with external calendar applications.
*   Photo verification for chore completion.
*   More granular permissions for chore management (e.g., admin approval for chores, editing any chore by admin).
*   Support for multiple distinct family units under a single user account.
*   Social login options (Google, Facebook, etc.).
*   Advanced chore attributes: categories/tags, estimated time to complete, specific instructions/sub-tasks.
*   Ability for users to propose chores that require admin approval.
*   More sophisticated handling of point calculation edge cases or customizable point systems by the family.
*   Deadline tracking with notifications (explicitly mentioned as potential enhancement by user).
