# Project Coding Tutor

A reusable ChatGPT Skill for learning software engineering **inside a real project** instead of finishing a long prerequisite course before touching the codebase.

It is designed for learners who already know some programming but have uneven depth across a stack — for example, a Java/Spring developer learning Python, FastAPI, LangGraph, tool calling, stateful Agents, reliability, evaluation, and interview-ready system design.

## What makes it different

This Skill optimizes for **delivery + mastery**:

- project-first, not lecture-first;
- teach only the next 1–2 core concepts needed for the current slice;
- use accurate analogies from technologies the learner already knows;
- let AI accelerate boilerplate while protecting learning time for high-value mechanisms;
- deliberately test failure modes instead of teaching only happy paths;
- require observable verification, not “the code looks right”;
- end meaningful sections with teach-back and interview compression;
- connect project milestones to learning notes without confusing CI success with mastery.

## Three help levels

### Level 1 — Hint

For deliberate practice and interview-style thinking. The tutor gives focused questions, clues, tiny examples, and failing tests before giving the final implementation.

Example:

> `Level 1，提示我怎么保证退款接口幂等，不要直接写答案。`

### Level 2 — Pair (default)

For normal project development. The tutor explains the mechanism, builds the minimum slice with you, lets AI handle repetitive wiring, and leaves one meaningful edit/decision for you.

Example:

> `用教学模式带我实现 LangGraph WAITING_USER 的恢复。`

### Level 3 — Deliver + Debrief

For deadlines or hard blockers. The tutor may implement the slice directly, but must then trace the critical path, explain the invariants/failure modes, and require a small modification or mastery check.

Example:

> `Level 3，先帮我修掉这个 checkpoint 恢复 bug，然后带我拆解为什么。`

## A-class vs B-class work

The Skill classifies work before spending teaching time.

**A-class — must understand:** state machines, transactions, idempotency, authorization, concurrency, timeout recovery, checkpoint/resume, HITL, tool boundaries, eval design, source of truth, architectural tradeoffs.

**B-class — AI may accelerate:** routine DTOs, repetitive CRUD wiring, fixtures, CSS polish, mechanical schema mapping, repetitive configuration and test data.

A normally mechanical task becomes A-class when it carries a project-specific invariant — for example, a database UNIQUE constraint that prevents duplicate refund requests.

## Teaching loop

For substantial core mechanisms:

1. Problem first
2. Minimal mental model
3. Bridge from known knowledge
4. Trace the end-to-end flow
5. Tiny isolated experiment when useful
6. Integrate into the real repository
7. Learner-owned modification/prediction
8. Intentional failure injection
9. Verify with tests/state/trace
10. Teach-back
11. Interview questions
12. Learning note / milestone mastery record

The Skill adapts the presentation; it does not mechanically print twelve headings for every small question.

## Java → Python / Agent bridges

Examples used when accurate:

| New concept | Familiar anchor |
|---|---|
| Pydantic model | Java DTO + validation |
| FastAPI dependency | request-scoped dependency/filter/interceptor concepts |
| Python Protocol / ABC | Java interface, with looser runtime semantics |
| LangGraph state | explicit workflow/state-machine context |
| Tool wrapper | typed application-service adapter |
| Checkpoint | persisted workflow execution state, **not** a business transaction |
| Context manager | try-with-resources for lifecycle cases |

The tutor must also explain where each analogy breaks.

## Repository layout

```text
project-coding-tutor/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── help-levels.md
    ├── core-vs-boilerplate.md
    ├── session-workflow.md
    ├── mastery-and-notes.md
    ├── git-milestones.md
    ├── interview-mode.md
    └── commerceagent-example.md
```

A packaged `skill.zip` is generated from this folder.

## Install in ChatGPT

Open your Skills library at `/skills`, upload `skill.zip`, and enable the Skill.

You can then use natural prompts such as:

- `用 Project Coding Tutor 带我做这个任务。`
- `Level 1，先提示我，不要直接实现。`
- `Level 2，带我边做边学 FastAPI + Pydantic。`
- `Level 3，先修好，然后强制我复盘关键机制。`
- `把这个任务按 A 类/B 类分一下，我应该重点学什么？`
- `这个 milestone 做完了，帮我做 mastery check 和面试复盘。`

## CommerceAgent example

For a Java + Python after-sales Agent project, the included reference maps learning roughly like this:

```text
M0  FastAPI / tool calling / checkpoint / DB privilege boundary
M1  refund E2E / idempotency / authoritative verification / baseline
M2  return / clarification / interrupt-resume / Agent-value cases
M3  human approval / replay / concurrency / crash recovery
M4  versioned policy reference / safe stop / injection boundary
M5  deterministic tests / repeated model eval / honest comparison
```

Each milestone is treated as two independent gates:

- **Delivery gate:** does the behavior actually work and have evidence?
- **Mastery gate:** can the learner explain and modify the important mechanism?

Passing one does not automatically pass the other.

## Design principles

- Do not block project progress just to preserve artificial difficulty.
- Do not confuse generated code with learned knowledge.
- Do not spend the learner's energy on low-value boilerplate.
- Do not invent project evidence or interview claims.
- Prefer vertical slices and failure-driven learning.
- Reduce tutor intervention as the learner sees the same concept again.

## Validation

The Skill is intended to be packaged and validated with OpenAI's Skill Creator tooling. The release `skill.zip` should contain one Skill entrypoint and remain directly uploadable.
