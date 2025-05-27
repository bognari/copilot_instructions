---
applyTo: '**'
---
# --- Project Workflow Strategy ---

## 1. Overview

This document defines the universal task lifecycle for this project. All personas (Architect, Developer, Reviewer) must operate according to these states and transitions. The primary tool for tracking tasks is **ConPort**, and tasks should be clearly identified by their type using a prefix in the `log_progress` description (e.g., `[Architecture]`, `[Developer]`).

## 2. Task States & Transitions

The workflow is a state machine that processes requirements from high-level architecture to reviewed, completed code.

### 2.1. [Architecture Task]

* **Actor:** The Architect
* **Purpose:** To decompose large, high-level user requirements into a manageable, detailed plan. This is the starting point for all new features.
* **Input:** A new user goal, feature request, or requirement from a source document (PRD/GDD).
* **Possible Actions & Transitions:**
    1.  **Decompose (`A -> A`):** If the task is too large to be understood or refined in one step, the Architect will break it down into several smaller, more focused **[Architecture Task]** entries. The parent task is completed only after a final review confirms its children cover all original requirements.
    2.  **Investigate (`A -> B`):** If there is a significant technical or architectural unknown that blocks planning, the Architect will create a **[Research Task]** to resolve it.
    3.  **Refine (`A -> C`):** If the task is clear and small enough to be actionable by a developer, the Architect will refine it into a **[Developer Task]**. This involves adding all necessary details to meet the "Definition of Ready" (DoR).

### 2.2. [Research Task]

* **Actor:** The Architect (or Developer, if the unknown is at the implementation level).
* **Purpose:** To resolve a specific, well-defined unknown and produce knowledge that unblocks planning or development.
* **Input:** A clear research question from a parent **[Architecture Task]**.
* **Possible Actions & Transitions:**
    1.  **Conclude (`B -> A`):** Once the research is complete, the findings are documented. The Architect then updates the parent **[Architecture Task]** with this new knowledge, allowing its refinement to continue.

### 2.3. [Developer Task]

* **Actor:** The Developer
* **Purpose:** To implement a single, well-defined feature slice using Test-Driven Development (TDD).
* **Input:** A task that meets the "Definition of Ready," including a clear Value Proposition, Acceptance Criteria, Non-Functional Requirements, and all dependencies.
* **Possible Actions & Transitions:**
    1.  **Implement:** The Developer follows the TDD cycle (Red-Green-Refactor) to write tests and production code until all acceptance criteria are met.
    2.  **Request Review (`C -> D`):** Once the implementation is complete and all local tests pass, the Developer transitions the task into a **[Review Task]**, signaling it is ready for verification.
    3.  **Rework (`D -> C`):** If a **[Review Task]** is rejected, the Developer receives it back with specific feedback and continues working on it.

### 2.4. [Review Task]

* **Actor:** The Reviewer (This can be a peer developer or the Architect).
* **Purpose:** To formally verify that the implemented code meets all acceptance criteria, NFRs, coding standards, and architectural guidelines.
* **Input:** A **[Developer Task]** that has been marked as complete and is ready for review.
* **Possible Actions & Transitions:**
    1.  **Approve (`D -> Close`):** If the implementation is correct, robust, and complete, the Reviewer approves it. The task's status is set to "DONE," and it transitions to the final **Close** state.
    2.  **Reject (`D -> C`):** If significant issues are found, the Reviewer rejects the submission, provides clear, actionable feedback, and transitions the task back to the **[Developer Task]** state for rework.

### 2.5. [Task Close]

* **Actor:** System/None
* **Purpose:** Represents the final, successfully completed state of a task. The work is considered finished and integrated.