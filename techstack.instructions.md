---
applyTo: "**"
---

# --- Global Tech Stack Overview ---

This document outlines project-wide standards and tool configurations. All personas must adhere to these rules.

### 1. Persona-Specific Guidelines

- **If you are The Architect, you MUST FULLY read (all 25 lines) for your specific guidelines:** `@/docs/architect_techstack.md`
- **If you are The Developer or The Reviewer, you MUST FULL read (all 50 lines) for your specific guidelines:** `@/docs/developer_techstack.md`

## 2. Global Architecture & Access Patterns

- **Static Typing: MANDATORY** for all GDScript code. Use specific types. Do not (pre)load scripts with `class_name`; use the class name directly as the type.
- **Modularity & SRP:** Design around the "Scene for What, Script for How" principle.
- **Decoupling:** Minimize direct dependencies between major systems (e.g., UI, GameState, Player). Your designs must prioritize communication via the global `EventBus` (Signals).
- **Composition over Inheritance:** Plan for complex objects to be built by composing smaller, independent scenes and nodes.
- **Autoloads (Singletons):** Access via global name ONLY (e.g., `EventBus`). **Do not use `get_node("/root/Name")`.** Scripts used as Autoloads in `project.godot` must not have a `class_name`.
- **Input Handling:** All player input must be handled via named actions defined in the **Input Map**.

## 3. Running Tests (`gdUnit4`)

- **Testing (`gdUnit4`): MANDATORY** that all non-trivial, non-private logic must be covered by unit tests.
- **Command:** `addons/gdUnit4/runtest.sh -a test/YourTestSuite.gd`
- **Note:** Ignore "Capture not registered" errors during test runs, as this is a known Godot engine bug.
