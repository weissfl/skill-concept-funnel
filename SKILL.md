---
name: concept-funnel
description: Concept processing. Manages the full cycle of designing and objectively evaluating hypotheses, solutions, or concepts based on user constraints.
---

START_concept_funnel

START_goal
### Goal
Ensure the generation and rigorous evaluation of viable hypotheses. The agent must maintain all options in a state of Superposition until the full audit is complete, providing the user with standardized, objective data (critique and score) for the final selection (Collapse) of the optimal solution that is guaranteed to fit the task constraints.
END_goal

START_task
### Task
The agent guides the system through 5 stages:
1. Initialization (context audit, identification of missing requirements and constraints).
2. Contract (translation of initial conditions into measurable Criteria).
3. PROPOSE and HOLD (generation of a Hypothesis pool strictly adhering to the Contract and holding them in Superposition).
4. EVALUATE (routing and launching the audit: Lite, Medium, High).
5. COLLAPSE-PREP (aggregation of standardized scores and transferring the final decision rights to the user).
END_task

START_environment
### Environment
* Context Gaps. By default, the user's initial prompt inherently contains semantic gaps. The agent is obliged to identify them before starting work.
* Runtime Constraints. The depth of the evaluation (EVALUATE) depends on the technical capability of the current platform to launch external sub-agents.
* Interactivity. The process requires mandatory checkpoints. Advancing to the next macro-phase without explicit user approval is strictly prohibited.
END_environment

START_working_patterns
### Working Patterns
The global routing operates as a finite state machine with strict transitions. Within the phases, a flexible iterative loop (dialogue and revisions) operates until user confirmation is received.

START_phase_init
TRIGGER: Skill initialization.
ACTION: Assess current context. Identify uncertainties. Query the user to crystallize constraints (e.g., budget, resources, business limits, tech stack, etc.).
GOAL: Approved Initial Conditions.
Rationale: The agent independently guessing constraints leads to the generation of irrelevant concepts.
END_phase_init

START_phase_contract
TRIGGER: Initial conditions received.
ACTION: Formulation of 3-5 fundamental evaluation criteria based on the initial conditions.
GOAL: Approved Contract (Criteria).
END_phase_contract

START_phase_propose_and_hold
TRIGGER: Contract approved.
ACTION: Enter Superposition. Generate a pool of hypotheses (PROPOSE) strictly adhering to the Contract. Keep all hypotheses completely equal (HOLD).
GOAL: User-approved pool of equal candidates for evaluation.
Rationale: Prematurely highlighting a favorite forces the model into a local optimum and devalues the objective audit.
END_phase_propose_and_hold

START_phase_evaluate
TRIGGER: Candidate pool approved.
ACTION: Request evaluation mode (Lite/Medium/High) from the user and execute the audit. Rule: All tasks, instructions, and context passed to sub-agents MUST be strictly in English. Regardless of the mode, the result of each evaluation must strictly follow the format: detailed <critique> (vulnerability check against Criteria) and a final <score> on a scale from 1 to 10.
GOAL: Obtain raw scores and critique in a unified format.

Evaluation Algorithms:
* lite: Evaluation runs in the current window. Rule: The critique phase must be extensive. Mandatory compression of the dialogue history before starting to retain attention focus.
* medium: Invocation of a single sub-agent. The Contract and ALL hypotheses are passed to it simultaneously. Returns a report following the strict evaluation format.
* high: Maximum isolation. Each hypothesis is evaluated in a separate, completely clean context by a dedicated sub-agent. Returns a report following the strict evaluation format.
END_phase_evaluate

START_phase_collapse
TRIGGER: Raw evaluations received in a unified format.
ACTION: Data aggregation. Formulation of a neutral final dashboard containing ONLY a summary table mapped to the criteria and the calculated total scores.
Rule: The agent acts strictly as a Secretary. The agent MUST remain in Superposition, maintaining absolute neutrality. It is strictly forbidden to provide any conclusions, summaries, or recommendations.
GOAL: The user independently makes a choice. Superposition collapses (Collapse).
Rationale: The choice (Collapse) is the human's area of responsibility. An agent imposing a decision or drawing analytical conclusions creates a confirmation bias loop.
END_phase_collapse

END_working_patterns

START_tactical_freedom
### Tactical Freedom
* Right to conduct iterative dialogue within phases, proposing adjustments.
* Right to independently choose the visual format (tables, bulleted lists) for the final report to maximize the readability of dry data.
END_tactical_freedom

START_completion_criteria
### Completion Criteria
* Success: The user made a choice (performed a Collapse) based on the provided neutral analytical dashboard.
* Rollback: The user rejected data at any stage. The agent logs the corrections and triggers a micro-cycle to regenerate the current phase.
* Fail-safe: Medium or High mode was selected, but the platform does not support sub-agents. The agent stops the process, outputs an error, and suggests Lite mode.
END_completion_criteria

END_concept_funnel