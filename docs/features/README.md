# Feature Documentation Workflow

## 1. Purpose

This folder (`/features`) holds all documentation related to a specific feature. The goal is to keep all technical, decision-making, and user-facing information organized and centralized.

For each new feature, a new **subfolder** should be created with its name. Example: `/features/user-management/`.

Within each subfolder, the documentation structure is as follows:

```
my-new-feature/
├── README.md       (End-User Guide)
├── spec.md         (Technical Specification for Development)
└── records/        (Technical Decision Records)
    └── ...
```

---

## 2. The Documentation Process

### Step 1: `spec.md` (Technical Specification)

Before starting to code, create a `spec.md` file in the root of the feature folder.

-   **Purpose:** To detail the feature's technical requirements, breaking down a large feature (Epic) into smaller User Stories. It serves as a prompt for the developer or AI agent.
-   **Template:**

````markdown
# Spec: [Epic/Feature Name]

## 1. Overall Objective
> (A high-level summary of the entire feature/epic.)

---

## 2. User Stories

### User Story #1: [Title of the first story]
> **As a** [user type], **I want to** [do something], **so that** [I can achieve some goal].

**Functional Requirements:**
- [ ] Requirement 1.1
- [ ] Requirement 1.2

**Technical Notes (if applicable):**
> (API endpoints, DB changes, or logic specific to THIS story).

---

### User Story #2: [Title of the second story]
> **As a** [user type], **I want to** [do something else], **so that** [I can achieve another goal].

**Functional Requirements:**
- [ ] Requirement 2.1
- [ ] Requirement 2.2

**Technical Notes (if applicable):**
> (API endpoints, DB changes, or logic specific to THIS story).

---
````

### Step 2: `records/` (Decision Records)

If important technical decisions are made during development, document them in the `records/` folder.

-   **Purpose:** To maintain a historical log of Architectural Decision Records (ADRs) so the team can understand the *why* behind certain technical choices.
-   **Files:** Create a `.md` file for each decision, using the format `YYYY-MM-DD-decision-title.md`.
-   **Template:**

````markdown
# Title: [Describe the decision]

- **Date:** YYYY-MM-DD
- **Status:** [Accepted | Deprecated]

## Context
> (What was the problem or situation?)

## Decision
> (What was the chosen solution?)

## Consequences
> (Describe the positive and negative outcomes of this decision).
````

### Step 3: `README.md` (End-User Guide)

Once the feature is developed, the main `README.md` file in the feature's root folder (e.g., `/features/user-management/README.md`) should contain the guide for the end-user.

-   **Purpose:** To explain in simple, non-technical terms how to use the functionality.
-   **Template:**

````markdown
# User Guide: [Feature Name]

### What is it for?
> (A simple explanation of the user benefit).

### How to use it
> (A step-by-step guide, ideally with images or GIFs).
1.  Step 1...
2.  Step 2...
````
