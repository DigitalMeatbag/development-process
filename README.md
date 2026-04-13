# Documentation-Driven Development and Convergence Process

A formal process for turning raw ideas into implemented systems with explicit control over correctness, coherence, completeness, documentation fidelity, and convergence quality. Designed for software engineering work where agentic systems participate materially in implementation, review, remediation, evaluation, planning, and handoff.

## Contents

| File | Description |
|---|---|
| [`process_foundation.md`](process_foundation.md) | Foundation Document v6 — philosophy, intent, constraints, non-goals, and high-level process shape |
| [`process_spec.md`](process_spec.md) | Process Specification v2 — formal behavioral contract derived from the foundation; normative requirements for every phase |

## Process at a Glance

```
clarify → specify → build → review → remediate → evaluate → plan → hand off → repeat
```

The process has eight phases:

1. **Intent Formation** — distill motivating driver into a foundation document
2. **Specification Formation** — derive a formal implementation spec from the foundation
3. **Build Execution** — implement against the spec
4. **Review** — evaluate implementation against spec, architecture, and quality standards
5. **Remediation** — resolve review findings at the root with minimal durable change
6. **Evaluation** — determine what is resolved, open, or requires follow-on work
7. **Cycle Planning** — decide: close, continue, re-scope, revise governing docs, or hand off
8. **Handoff** — package cycle outcome for the next team, owner, or time-shifted collaborator

Phases 4–8 form the **convergence loop**, which repeats until closure is earned.

## Core Philosophy

- Explicit intent over implied intent
- Living documents over frozen documents
- Contract-driven implementation over improvisation
- Root-cause correction over local patching
- Earned closure over apparent progress
- Convergence over endless motion
- Process artifacts as truth over tool state as truth

## Applicability

Works in both **greenfield** and **brownfield** contexts. In brownfield work, the existing codebase is the environment the work occurs within — not a prerequisite to fully document before starting. Scope is defined by what the motivating driver touches.

The process is **tool-agnostic**. Issue trackers and project boards may support visibility, but process artifact state is always authoritative over tool state.
