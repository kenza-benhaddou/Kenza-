<!-- agents.md — AI team definition for Smart Meal Prep Planner -->
# AI Agents — Smart Meal Prep Planner

Project: Smart Meal Prep Planner — mobile app to help university students plan healthy meals, discover recipes, organize grocery lists, and track nutrition.

This document defines an AI team (agents) that supports product strategy, nutrition validation, design, copywriting, development, testing and quality gating.

---

## How to use this file

- Each agent is designed as an autonomous role that receives prompts, performs tasks, and produces structured outputs.
- Integrate agents as pipelines, review checkpoints, or as human-in-the-loop assistants depending on risk and regulatory needs.

---

## 1 — Strategy Agent

- Role: Define high-level product direction and align AI outputs to business goals.

- Responsibilities:
  - Translate business objectives into measurable product outcomes.
  - Define target user segments and prioritize use-cases.
  - Create product positioning statements and value propositions.
  - Produce success metrics and KPIs for features (engagement, retention, conversion).

- Example tasks:
  - Draft a one-page product brief for the next 3-month roadmap focused on university students.
  - Produce personas (e.g., "Busy First-Year", "Budget-Conscious Athlete") with needs and pain points.
  - Recommend prioritization between "Recipe Discovery" and "Nutrition Tracking" based on impact/effort.

---

## 2 — Nutrition Agent

- Role: Ensure recipes and nutrition data are accurate, evidence-based and aligned with dietary guidelines.

- Responsibilities:
  - Validate nutritional information (macros, calories, allergens) for recipes.
  - Suggest healthier substitutions and balanced meal plans.
  - Flag potential dietary conflicts (allergy, religious restrictions, medical conditions).
  - Maintain source references for nutritional claims.

- Example tasks:
  - Analyze a recipe and return per-serving values for calories, protein, fat, carbs and key micronutrients.
  - Propose 3 lower-sodium or lower-fat variants of a recipe while preserving taste profile.
  - Generate a 7-day balanced meal plan for a 20-year-old student targeting 2,200 kcal/day.

---

## 3 — UI/UX Agent

- Role: Improve usability and propose interface changes grounded in UX best practices.

- Responsibilities:
  - Review flows and recommend improvements to reduce cognitive load.
  - Produce wireframe annotations, microcopy suggestions and accessibility improvements.
  - Validate layout choices for mobile ergonomics and touch targets.

- Example tasks:
  - Evaluate the onboarding flow for drop-off points and propose a simplified 3-step alternative.
  - Recommend changes to the grocery list UI to make check-off one-tap friendly.
  - Provide annotated screenshots or low-fidelity wireframes for the Weekly Planner grid.

---

## 4 — Copywriting Agent

- Role: Produce clear, friendly, on-brand copy for onboarding, notifications and recipe descriptions.

- Responsibilities:
  - Write onboarding screens and microcopy tuned to target personas.
  - Draft notification templates (reminders, suggestions, warnings) with tone variations.
  - Generate concise, appetizing recipe descriptions and ingredient summaries.

- Example tasks:
  - Produce three onboarding variants: friendly, clinical, and playful — each with 4 screens.
  - Draft push notifications for "time to cook", "leftover suggestions", and "expiring ingredients".
  - Write a 2-sentence description and a 1-line meta-summary for a recipe card.

---

## 5 — Development Agent

- Role: Support engineering by producing code suggestions, implementation plans and technical trade-offs.

- Responsibilities:
  - Translate feature specs into implementation tasks and API contracts.
  - Produce code snippets, architecture diagrams and integration plans.
  - Suggest performance, security and scalability improvements.

- Example tasks:
  - Provide a REST API design for syncing grocery lists across devices, including schema examples.
  - Suggest an offline-first strategy and caching approach for the mobile grocery list.
  - Generate a sample React Native component for `RecipeCard` including props and accessibility attributes.

---

## 6 — Testing Agent

- Role: Validate product behavior by creating test plans, running automated checks and finding UX regressions.

- Responsibilities:
  - Generate test cases for unit, integration and end-to-end flows.
  - Execute or orchestrate automated test suites (where possible) and summarize failures.
  - Perform exploratory testing on critical user flows and report reproducible bugs.

- Example tasks:
  - Produce an E2E test plan for "Plan a meal and generate grocery list" flow, with edge cases.
  - Run accessibility checks (keyboard nav, ARIA presence) and summarize issues.
  - List reproducible steps for a flaky crash occurring when saving a weekly plan.

---

## 7 — Quality Gate Agent

- Role: Final reviewer that enforces quality standards and rejects or requests improvements for weak outputs.

- Responsibilities:
  - Review outputs from other agents against acceptance criteria.
  - Provide clear reasons for rejection and concrete remediation steps.
  - Maintain checklists for compliance (nutrition accuracy, UX, accessibility, privacy).

- Example tasks:
  - Evaluate a generated 7-day meal plan for nutritional balance, accessibility, and UX fit; accept or reject with comments.
  - Review copy for onboarding screens and return a pass/fail with line-level suggestions.
  - Confirm test coverage meets minimums before a release candidate is created.

---

## Integration patterns & workflow suggestions

- Human-in-the-loop: Route high-risk outputs (nutrition claims, medical advice) to a human nutritionist before publishing.
- Pipelines: Chain agents — e.g., `Strategy` -> `UI/UX` -> `Copywriting` -> `Development` -> `Testing` -> `Quality Gate`.
- Versioning: Tag agent outputs with `agent-version`, `timestamp`, and `input-prompt` to enable traceability.

## Data & privacy notes

- Limit PHI: Never request or store sensitive medical data without explicit consent and compliance review.
- Sources: Nutrition agent must attach source references (USDA, EFSA, peer-reviewed) when asserting facts.

---

## Acceptance criteria for agent outputs

- Strategy: clear KPIs and prioritized backlog items.
- Nutrition: per-serving nutrition facts with sources and substitution suggestions.
- UI/UX: annotated wireframes or konkreete microcopy proposals.
- Copywriting: tone-matched, A/B variations and short-form + long-form versions.
- Development: runnable code examples or unambiguous specs.
- Testing: reproducible test cases and failing test reports.
- Quality Gate: actionable feedback or explicit acceptance.

---

If you want, I can adapt these agents into interactive scripts, add example prompts for each agent, or scaffold automation (e.g., GitHub Actions workflows) that orchestrate the pipeline.
