---
applyTo: "**"
---

# --- Project Workflow Strategy ---

Universal task lifecycle for Architect, Developer, Reviewer. Tool: **ConPort**. Task type prefix in `log_progress` e.g. `[Architecture Task]` (AT) and `[Developer Task]` (DT)
**"Sprint" Definition:** Work a Developer persona fully implements in one interaction (prompt-response cycle). This defines DT target scope

For details you MUST FULLY read (all 50 lines) `@/.docs/workflow.md`

```mermaid
graph TD
    Start("New Req/GDD") --> AT_TODO(["[ArchTask] (TODO)"]);
    subgraph "Architect Phase"
        AT_TODO -- "Start Work" --> AT_IN_PROGRESS(["[ArchTask] (IN_PROGRESS)"]);
        AT_IN_PROGRESS -- "Research Needed" --> AT_IN_RESEARCH(["[ArchTask] (IN_RESEARCH)"]);
        AT_IN_RESEARCH -- "Research Done" --> AT_IN_PROGRESS;
        AT_IN_PROGRESS -- "Decompose" --> AT_REPLACED(["Parent AT (REPLACED)"]);
        AT_IN_PROGRESS -- "Decompose" --> AT_TODO;
        AT_IN_PROGRESS -- "Refine" --> AT_REFINED(["Parent AT (REFINED)"]);
        AT_TODO -- "Req. Change" --> AT_CANCELED(["[ArchTask] (CANCELED)"]);
        AT_IN_PROGRESS -- "Req. Change" --> AT_CANCELED;
        AT_IN_RESEARCH -- "Req. Change" --> AT_CANCELED;
        AT_REFINED -- "Req. Change" --> AT_CANCELED;
    end
    subgraph "Dev & Review Cycle"
        AT_IN_PROGRESS -- "Refine" ----> DT_TODO(["New [DevTask] (TODO)"]);
        DT_REJECTED(["[DevTask] (REJECTED)"]) -- "Start Rework" --> DT_IN_PROGRESS(["[DevTask] (IN_PROGRESS)"]);
        DT_TODO -- "Start Work" --> DT_IN_PROGRESS;
        DT_IN_PROGRESS -- "Implementation Done" --> DT_IN_REVIEW(["[DevTask] (IN_REVIEW)"]);
        DT_IN_REVIEW -- "Approved" --> DT_DONE(["[DevTask] (DONE)"]);
        DT_IN_REVIEW -- "Rejected" --> DT_REJECTED;
        DT_TODO -- "Req. Change" --> DT_CANCELED_DEV(["[DevTask] (CANCELED)"]);
        DT_IN_PROGRESS -- "Req. Change" --> DT_CANCELED_DEV;
        DT_IN_REVIEW -- "Req. Change" --> DT_CANCELED_DEV;
        DT_REJECTED -- "Req. Change" --> DT_CANCELED_DEV;
    end
```
