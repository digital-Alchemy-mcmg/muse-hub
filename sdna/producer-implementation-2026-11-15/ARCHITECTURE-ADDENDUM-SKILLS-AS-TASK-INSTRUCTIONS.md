# ARCHITECTURE ADDENDUM

## Skills as Reusable Task Instructions

### SDNA — Workflow and Agent Execution Clarification

Status: separate memo for the architecture documentation, implementing Decision 4 of the Operator Directive — Four Approved Decisions, Amazon Quick Skills — Producer Skill Revision, 2026-11-15. Its purpose is to prevent future agents and models from repeatedly confusing task instructions with architectural components. It clarifies the use of Skills. It does not change the authority hierarchy, module ownership, function register, workbook contracts, or operator decision rights. It does not authorize modifications to the authoritative construction specification.

### 1. PURPOSE

Clarify the role of Skills within the SDNA workflow.

Skills are reusable, self-contained task instructions supplied to agents to perform specific assignments.

They are not independent architectural modules, new system components or additional layers of the Evidence Foundry.

### 2. WHAT A SKILL IS

A Skill is essentially a saved, reusable prompt.

It encapsulates:

- The task to perform.
- Required inputs.
- The procedure to follow.
- Expected output.
- Acceptance criteria.
- Failure and stop conditions.

Its purpose is to eliminate repetitive operator prompting.

Instead of manually entering detailed instructions every time an agent performs a recurring task, the workflow invokes the corresponding Skill.

### 3. INDEPENDENCE

Each Skill must be understandable and executable independently.

An agent using a particular Skill does not need to understand the entire SDNA architecture.

It does not need to know how other Skills operate or what happens after its assigned task.

A Skill is responsible for performing its own assignment correctly.

Its required input and output contracts are sufficient to define its task boundary.

### 4. WORKFLOW ORCHESTRATION

The workflow determines when a Skill is invoked and supplies the necessary input.

The workflow may invoke multiple Skills in sequence, passing the appropriate completed artifact from one operation to another.

This does not mean that each individual Skill must understand the entire sequence.

**Workflow orchestration belongs to the workflow. Task execution belongs to the Skill.**

The operator should not need to repeatedly supply the detailed prompt instructions that the Skills already contain.

### 5. ARCHITECTURAL BOUNDARY

Do not treat the existence of a Skill as authorization to introduce:

- New architecture modules.
- New system dependencies.
- New agent responsibilities.
- Unnecessary upstream or downstream awareness.
- Additional integration requirements.
- Architectural assumptions inside otherwise standalone task instructions.

A Skill may define what it needs and what it produces.

It must not acquire responsibilities merely because another system eventually uses its output.

### 6. PRESERVATION OF AUTHORITY

This addendum clarifies the use of Skills. It does not change the authority hierarchy, module ownership, function register, workbook contracts or operator decision rights.

It does not authorize modifications to the authoritative construction specification.

Existing architectural responsibilities remain where they were assigned.

### 7. DESIGN PRINCIPLE

Skills are task-level instruction packages.

They make agents repeatably capable of performing defined jobs without requiring the operator to enter the same instructions repeatedly.

The architecture provides the environment in which workflows operate.

The workflow invokes the Skills.

The Skills execute their assigned tasks.

**A Skill is a reusable prompt, not another architecture.**

**The distinction to preserve going forward:** the architecture tells us what the system is; the workflow determines which job gets performed; the skill tells the agent exactly how to perform that job.

That separation is what prevents this same confusion from propagating into the remaining skills.
