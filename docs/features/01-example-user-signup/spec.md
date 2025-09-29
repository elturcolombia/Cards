# Spec: Google Authentication

## 1. Overall Objective

To allow users to sign up and log into the application using their Google account, providing a secure, password-less, and seamless experience.

---

## 2. User Stories

### User Story #1: New User Registration
> **As a** first-time visitor, **I want** the system to automatically create an account for me when I sign in with Google, **so that** I don't have to fill out a manual registration form.

**Functional Requirements:**
- [ ] A "Sign in with Google" button must be present on the login page.
- [ ] Clicking the button redirects to Google's OAuth consent screen.
- [ ] On callback from Google, the system checks that no user exists with the provided Google ID.
- [ ] A new user record is created in the `users` table.
- [ ] The `name`, `email`, `google_id`, and `avatar` fields are populated from the data provided by Google.
- [ ] The user is automatically logged in.
- [ ] The user is redirected to the application dashboard.

**Technical Notes:**
- This flow is handled by the `handleGoogleCallback` method in the `AuthController`.
- It involves an `INSERT` operation on the `users` table.
- The `password` field for the new user will be `null`.

---

### User Story #2: Returning User Login
> **As a** returning user, **I want** the system to recognize me and log me in when I use the "Sign in with Google" button, **so that** I can access my account quickly.

**Functional Requirements:**
- [ ] The login flow is initiated by the same "Sign in with Google" button.
- [ ] On callback from Google, the system finds an existing user in the `users` table matching the provided `google_id`.
- [ ] The user's `name` and `avatar` may be updated if they have changed in their Google profile.
- [ ] The user is logged into their existing account.
- [ ] The user is redirected to the application dashboard.

**Technical Notes:**
- This flow is also handled by the `handleGoogleCallback` method in the `AuthController`.
- It involves a `SELECT` and potentially an `UPDATE` operation on the `users` table.

---

## 3. Shared Technical Implementation

### Database Changes

- The `users` table requires the following columns to be added via a migration:
  - `google_id` (string, nullable, unique)
  - `avatar` (string, nullable)
  - `password` (must be made nullable)

### API / Web Endpoints

- **`GET /auth/google/redirect`**
  - **Description:** Initiates the authentication flow for both registration and login.
  - **Action:** Redirects the user to the Google OAuth page.

- **`GET /auth/google/callback`**
  - **Description:** Handles the callback from Google for both registration and login.
  - **Action:** Contains the core logic to differentiate between a new and a returning user.
