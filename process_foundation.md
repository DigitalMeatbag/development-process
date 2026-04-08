# Process Foundation Document v6

> **Purpose:** This is the sixth iteration of the living foundation document for the documentation-driven development and convergence process. It preserves the intent of earlier versions while incorporating resolved gaps from v5: packet depth scaling by consequence, the spike mechanism, an explicit tooling policy, a sharpened brownfield entry model, and explicit agent failure mode governance.  It remains pre-spec, but it is intended to be strong enough to govern the drafting of a formal process specification.

---

## Intent

This process exists to turn raw ideas into implemented systems with tighter control over correctness, coherence, completeness, documentation fidelity, and convergence quality.

It is defined primarily for software engineering work, especially where agentic systems participate materially in implementation, review, remediation, evaluation, planning, and handoff. Its control structure may generalize to other domains, but this document is optimized for software delivery contexts and team-scale professional use.

It is intended to apply in both greenfield and brownfield environments. Brownfield work is always motivated by something specific — a feature, a rework, a migration, a compliance requirement. That motivation seeds the foundation document the same way greenfield intent does. The scope of brownfield work is defined by what the motivation touches, not by the full extent of the existing codebase. The existing codebase is the environment the work occurs within — it surfaces as a source of constraints, coupling risks, and discovered findings during the process, not as a prerequisite to fully document before work begins. The process must therefore remain usable under conditions of legacy coupling, incomplete documentation, existing ownership boundaries, and uneven cross-team turnaround times.

In software delivery contexts, `git` is the default version-control and change-tracking substrate for governed artifacts. It supports traceability, revision history, and inspectable deltas, but it does not define process semantics, routing, or closure standards.

The process is meant to support work where:
- ideas and constraints are initially incomplete
- design intent needs to be made explicit before implementation
- implementation should be grounded in living documentation rather than ad hoc inference
- post-build iteration must reduce churn rather than merely react to defects

The process is designed to produce not only working code, but also a stable chain of reasoning from intent to implementation to closure.

It must also preserve traceability across cycles so that progress, drift, and churn can be distinguished from one another.

---

## Philosophy

Prefer explicit intent over implied intent.  
Prefer living documents over frozen documents.  
Prefer contract-driven implementation over improvisation.  
Prefer root-cause correction over local patching.  
Prefer earned closure over apparent progress.  
Prefer convergence over endless motion.  
Prefer stable issue identity over cycle-local phrasing.  
Prefer explicit routing over implicit override behavior.  
Prefer coherent work units over arbitrary task slicing.  
Prefer front-loaded unknowns over mid-cycle discovery.  
Prefer process artifacts as truth over tool state as truth.

This process assumes that a build is not the end state. A build is a candidate reality that must be challenged and refined until it aligns with intent, specification, implementation quality standards, and documentation truth.

---

## Non-Goals

- Not intended to optimize for the fastest possible path to initial code generation
- Not intended to minimize documentation work at the expense of clarity
- Not intended to rely on the codebase itself as the primary design record
- Not intended to treat review as a one-time gate
- Not intended to reward visible effort in place of demonstrable closure
- Not intended to produce static, unchanging documents
- Not intended to allow issue tracking to become informal, transient, or implicit across cycles
- Not intended to allow silent override, undocumented exception paths, or implicit closure claims
- Not intended to force one fixed work size across all phases, teams, or operating contexts
- Not intended to treat tooling state as a substitute for process authority, finding identity, or closure discipline

---

## Core Process Shape

The process currently has eight major phases:

1. **Intent formation**
   - Raw ideas, constraints, invariants, tradeoffs, and non-goals are explored and distilled into a foundation document.

2. **Specification formation**
   - The foundation document is used to derive a formal implementation specification.
   - The spec is iterated until it is precise enough to govern implementation.

3. **Build execution**
   - Implementation agents build against the spec and repository guidance.

4. **Review**
   - A review agent evaluates the implementation against the governing specification, architecture, SOLID, completeness, correctness, coherence, and documentation accuracy.

5. **Remediation**
   - A remediation agent resolves review findings at the root and with minimal durable change.

6. **Evaluation**
   - An evaluation agent assesses the remediation against the most recent prior review and determines what is actually resolved, what remains open, and what new follow-on work must be planned.

7. **Cycle planning**
   - A planning step determines whether to close the cycle, continue remediation, re-scope findings, revise governing documents, or start a new cycle packet.

8. **Handoff / repetition**
   - When work must move to another receiving context, a handoff step packages the cycle outcome for the next team, owner, or non-local collaborator before repetition continues.

The process is not complete unless each phase produces explicit artifacts that can be inspected by the next phase.

A spike may be triggered during specification formation or build execution when a specific blocking unknown prevents scoping or design from proceeding. A spike is not a phase — it is a diagnostic mechanism that surfaces insufficient definition in the governing documents. See the Spike Guidance section.

---

## High-Level Flow

The process can be summarized as:

**intent -> contract -> implementation -> challenge -> convergence**

Or, more operationally:

**clarify -> specify -> build -> review -> remediate -> evaluate -> plan -> hand off when needed -> repeat as needed**

Each phase exists to reduce a different kind of uncertainty:

- Foundation reduces uncertainty about intent
- Spec reduces uncertainty about required behavior
- Build reduces uncertainty about implementability
- Review reduces uncertainty about defects and mismatches
- Remediation reduces uncertainty about corrective action
- Evaluation reduces uncertainty about closure status
- Cycle planning reduces uncertainty about what to do next
- Handoff reduces uncertainty for the next receiving context

---

## Core Granularity Concepts

### Work unit granularity
Work unit granularity is the size and coherence of the unit being processed through a cycle.

It determines how much change, reasoning, and evidence are grouped together for implementation, review, remediation, evaluation, and planning.

The preferred unit is not defined by file count, branch count, prompt count, or arbitrary effort size. It is the smallest coherent unit that can honestly support:
- one dominant objective
- one meaningful contract surface
- one intelligible remediation story
- one evaluable closure claim

### Review scope
Review scope is the boundary the reviewer inspects when assessing a work unit.

Review scope is related to work unit granularity but is not identical to it. A narrow work unit may require broad review if coupling, downstream effects, or contract instability demand it.

### Handoff granularity
Handoff granularity is the size and packaging of work as presented to another team, owner, or time-shifted collaborator.

Handoff granularity may legitimately be coarser than local execution granularity when cross-team communication cost, timezone delay, ownership boundaries, or integration context make fragmented handoff inefficient or misleading.

When work is rolled up for handoff, lineage to the underlying local work units must remain explicit.

### Packet depth
Packet depth is the level of required structure and completeness for a given cycle's packets.

Packet depth scales with consequence, not with process position. It must be determinable from information the process already requires at the start of a cycle. If packet depth cannot be determined, the work is not ready to advance.

Full packet depth is required when:
- the work carries non-trivial risk, or
- business value is sufficient that mitigation overhead is justified by the cost of a mistake

Scaled-back packet depth is permitted only when all three of the following hold:
- decisions are already made — the work is implementation only, with no meaningful decision points remaining
- the change is reversible
- mistakes are cheap to recover from — the cost of error in effort and money is low

Scaled-back packets must still produce explicit artifacts sufficient for the next phase to consume without reinterpretation. They may omit optional fields and compress multi-packet cycles into a single lightweight record, but they may not omit the minimum required contents for closure determination.

---

## Roles of the Main Artifacts

### Foundation document
Purpose:
- capture intent
- preserve constraints
- record philosophy
- record non-goals
- preserve closed decisions and rationale
- provide the upstream source for the spec

The foundation document answers:
- What kind of system are we building?
- What are its boundaries?
- What tradeoffs have been accepted?
- What should it explicitly not become?

### Specification
Purpose:
- define the implementation contract
- provide authoritative behavioral and architectural requirements
- define acceptance criteria
- define testing expectations
- govern implementation and review

The spec answers:
- What exactly must be built?
- How must it behave?
- What counts as correct, complete, and acceptable?

### Build artifacts
Purpose:
- embody the current candidate implementation
- serve as the thing being reviewed, remediated, and evaluated

### Git history
Purpose:
- provide durable version history for governed artifacts
- expose inspectable diffs for document and implementation changes
- support traceability between findings, packets, and concrete repository state

Git history may provide evidence for the process, but it does not replace packet structure, finding records, or closure decisions.

### Finding record
Purpose:
- preserve durable issue identity across cycles
- hold current status, severity, scope, rationale, and lineage
- prevent issue identity drift caused by paraphrase or reframing

Each finding record must include at minimum:
- a durable ID
- originating cycle
- title
- severity
- governing source reference
- affected area
- current status
- closure criteria
- lineage notes if the item was merged, split, or re-scoped

### Review packet
Purpose:
- package the review scope, governing inputs, findings, and evidence in a form that remediation and evaluation can consume without reinterpretation

### Remediation packet
Purpose:
- explain how findings were addressed
- expose root cause analysis, impacted areas, self-review, and resolution gate status

### Evaluation packet
Purpose:
- determine closure status for each prior finding
- identify downstream effects, documentation drift, and test insufficiency
- produce a clean planning input for the next cycle

### Planning packet
Purpose:
- record the routing decision after evaluation
- define whether the cycle closes, continues, re-scopes, triggers document revision, or requires handoff
- define the starting conditions and scope assumptions for the next cycle

The planning packet answers:
- What is the next action?
- Why was that route selected?
- Which findings remain active, transformed, deferred, or closed?
- What governing artifacts must change before the next cycle begins?

### Handoff packet
Purpose:
- package a cycle outcome for another team, owner, or non-local receiving context
- preserve the larger thread when external or higher-risk non-local transfer would otherwise force reconstruction
- provide a receiver-facing summary plus references to the underlying governed artifacts rather than duplicating them in full

The handoff packet answers:
- What is being handed off?
- Who or what is the receiving context?
- Why is the handoff occurring now?
- What findings, lineage, and evidence matter to the receiver?
- What review, integration, acceptance, or follow-on work is expected next?

---

## Invariants

The following invariants currently appear essential to the process:

- Intent should be made explicit before implementation begins.
- The specification is the authoritative implementation contract.
- All governing documents are living documents and may be revised when necessary.
- Code must not be treated as authoritative over the specification.
- Review must be evidence-based and specification-grounded.
- Remediation must target root causes, not only visible symptoms.
- A finding is not resolved merely because a code change occurred.
- A finding is resolved only if the affected area would survive the next rigorous review without predictable, avoidable follow-on findings.
- Documentation and comments are part of the implementation surface and must remain aligned with behavior.
- Tests are supporting evidence of resolution, not proof by themselves.
- Repeated churn may indicate ambiguity or incompleteness in the governing documents, not only defects in the code.
- Findings must retain durable identity across cycles even when wording, scope, ownership, or structural relationship changes.
- Every cycle must produce artifacts explicit enough that a new participant could reconstruct the state of the work.
- No routing or closure decision should rely on undocumented override behavior.
- Version-control workflow must not be treated as a substitute for process reasoning, packet evidence, or closure discipline.
- Work unit granularity must be chosen by coherence and evaluability, not by arbitrary volume alone.
- Handoff granularity may differ from local execution granularity, but lineage between them must remain explicit.
- `split` and `merged` findings are transformed lineage states, not implicit closure states.
- Packet depth must be determinable before a cycle begins. If it cannot be determined, the work is not ready to advance.
- Spikes must be front-loaded. A spike triggered during build carries a mandatory pause on all related and downstream work.
- Process artifacts are the authoritative record. Tool state does not determine closure, routing, or finding identity.
- Out-of-scope work discovered at review signals that scope was not defined sufficiently for work to have started.
- Agent output conflicts are not resolved by agents. They require human adjudication.

---

## Decision Points

### 1. Foundation stability
The foundation is ready to feed the spec when:
- core intent is stable
- major constraints are explicit
- key non-goals are explicit
- major tradeoffs are recorded
- no unresolved high-level design ambiguity remains that would invalidate specification work

### 2. Specification readiness
The specification is ready to feed implementation when:
- required behavior is explicit
- architectural boundaries are explicit
- error model is defined
- important edge cases are covered
- acceptance criteria are concrete enough to review against

### 3. Implementation readiness for review
The implementation is ready for review when it is a meaningful candidate against the current specification, rather than an incomplete sketch.

### 4. Work unit granularity selection
The selected local work unit granularity is appropriate when:
- the unit has one dominant objective
- the unit maps to one coherent contract-bearing surface
- remediation can be explained as one intelligible story
- evaluation can make a truthful closure determination without hand-waving
- the unit is small enough to reason about locally but large enough to avoid artificial fragmentation

### 5. Packet depth selection
Packet depth is appropriate when:
- it can be determined from information already available at the start of the cycle
- it is honestly calibrated to the risk and business value of the work
- even at scaled-back depth, minimum required contents for closure determination are preserved

If packet depth cannot be determined, the work is not ready to advance.

### 6. Spike trigger
A spike is warranted when:
- a specific blocking unknown prevents scoping or design from proceeding
- the unknown cannot be resolved by further iteration on existing governing documents alone

A spike is not warranted when:
- the blocking unknown is a result of insufficient effort on foundation or spec work
- the intent is to defer scoping work rather than resolve a genuine unknown

### 7. Handoff granularity selection
The selected handoff granularity is appropriate when:
- the receiver can preserve the larger thread without excessive reconstruction cost
- the package is coarse enough to reduce coordination friction
- the package remains truthful about the underlying local work units and their lineage
- the receiver can determine what review, integration, or acceptance work is expected next

### 8. Post-evaluation routing
After evaluation, the process must choose whether to:
- close the cycle because closure was earned
- run another remediation cycle because implementation gaps remain
- re-scope findings because the real issue is broader or differently shaped than originally framed
- revise the specification or foundation because repeated churn indicates ambiguity, tension, or incompleteness in the governing documents
- prepare a handoff because the next receiving context is meaningfully non-local

### 9. Governing document revision trigger
The process must prefer document revision over repeated remediation when:
- multiple cycles produce materially similar findings
- remediation quality is adequate but review pressure keeps exposing the same ambiguity
- evaluators cannot determine closure because the governing docs are silent or internally tense
- scope disputes recur because the contract is not sharp enough

---

## Granularity Guidance

Work unit granularity should be dynamic rather than fixed.

As uncertainty narrows, granularity should usually become finer:
- earlier cycles may use coarser units because the primary task is clarifying intent, shaping boundaries, or stabilizing the contract
- later cycles may use finer units because the primary task is targeted remediation, closure, and regression prevention

Granularity should be influenced by the operating environment:
- greenfield work may tolerate coarser early units because architectural boundaries are still being formed
- brownfield work often requires finer local units because coupling, legacy behavior, and integration risk are harder to predict
- cross-team and cross-timezone collaboration may require coarser handoff granularity even when local execution granularity remains fine

The process should avoid two failure modes:
- units that are too large to support truthful closure claims
- units that are so small that coherence is lost and context must constantly be re-stitched

---

## Spike Guidance

A spike is a time-boxed investigation triggered when a specific blocking unknown prevents scoping or design from proceeding. It is not a phase in the process — it is a diagnostic mechanism that surfaces insufficient definition in the governing documents.

### When a spike is triggered
A spike may surface during specification formation when the foundation has not provided enough clarity to design a contract. It may surface during build execution when the spec has not provided enough clarity to implement against. In both cases the spike signals that an upstream governing document requires revision before work can continue.

A spike should not be invoked to defer scoping effort, explore general curiosity, or avoid committing to a design. It is only warranted when a genuine blocking unknown exists that cannot be resolved by further iteration on the governing documents alone.

Spikes should be front-loaded into the earliest possible stage of the process. The cost of a late spike is proportionally higher than an early spike.

### Spike inputs
- A clearly stated blocking unknown
- A declared time-box
- A reference to the governing document whose insufficiency triggered the spike

### Spike outputs — exactly one of three
1. **Unblocked** — investigation produced enough clarity to proceed to scoping or specification revision
2. **Blocked** — work cannot continue; reason and implications explicitly documented
3. **Decision point** — continuation is possible but not automatic; requires explicit human go/no-go with justification

### Late spike cost
A spike triggered during build carries a mandatory pause on all work related to or downstream of the affected area. This pause persists until the spike resolves and the governing documents are revised. This cost is intentional. It is the negative feedback for insufficient upfront definition and is not to be mitigated by continuing downstream work in parallel with an open spike.

---

## Tooling Policy

Tooling is explicitly out of scope for process definition.

Process artifacts — foundation documents, specifications, finding records, review packets, remediation packets, evaluation packets, planning packets, and handoff packets — are the authoritative record of process state. No tool's representation of work supersedes them.

Tools such as ADO, Jira, Linear, or GitHub Issues are communication surfaces. They are most effectively leveraged for visibility to business stakeholders and team members outside the core engineering process. They offer one perspective into ongoing work, not an authoritative or complete one.

Tool state does not determine closure, routing, or finding identity. A finding is not closed because an issue tracker marks it resolved. A cycle is not complete because a sprint board shows it done. A routing decision is not made because a ticket was moved to a queue.

The process is designed to be tool-agnostic. Tooling choices are made at the team or organization level and are not governed by this document. If tooling changes, the process does not change. If tool state conflicts with process artifact state, process artifact state is authoritative.

---

## Review Scope Discipline

Review scope must be explicit. Every review must declare one of the following modes:

- **Broad review**
  - Intended to assess the candidate holistically against the governing contract.
  - Appropriate for major milestones, first reviews, architectural changes, or when confidence in local boundaries is low.

- **Delta review**
  - Intended to assess only the changed area plus predictable impact surfaces.
  - Appropriate for targeted remediation cycles where issue identity is stable and scope discipline is important.

Scope may widen during review only when one of the following occurs:
- a finding cannot be understood without inspecting adjacent abstractions
- the changed area has obvious downstream callers or dependents
- evidence suggests that the stated issue is only a local manifestation of a broader defect
- documentation drift appears to invalidate the claimed contract

If scope widens, the reviewer must state:
- why widening was necessary
- what new boundary was included
- whether the widened scope created new findings or recontextualized existing ones

Out-of-scope work discovered during review must be flagged and removed. If scope cannot be determined well enough to identify what is out of scope, scope was not defined sufficiently for work to have started. The work and all downstream work must be paused and re-scoped before build resumes.

---

## Handoff Guidance

Local execution granularity and external handoff granularity do not need to be identical.

When handing work to another team or owner, the process should package the work at a granularity that preserves the larger thread well enough for the receiver to review, integrate, or accept it without excessive reconstruction cost.

A handoff packet is required for external handoff to another team, owner, or materially separate receiving context.

A handoff packet is optional but allowed for any other non-local handoff when continuity risk, async delay, ownership separation, or auditability needs justify formal packaging.

Coarser handoff packaging is especially appropriate when:
- teams have significant timezone separation
- review turnaround is expensive
- ownership boundaries require more context to evaluate integration correctly
- fragmented delivery would obscure the larger architectural or behavioral thread
- the receiver is expected to act without relying on local conversational continuity

A rolled-up handoff must still preserve:
- lineage to underlying work units
- finding identity
- truthful closure and non-closure claims
- evidence links to relevant diffs, packets, and governing documents

---

## Issue Identity And Tracking

Findings must have durable IDs across cycles.

The default ID format is:

`<domain>-<area>-<number>`

Example:

`PROC-TRACK-001`

The exact naming scheme may evolve, but the following rules are invariant:
- an ID is assigned when a finding first becomes explicit
- the ID survives wording changes across review, remediation, evaluation, planning, and handoff
- a finding may be split into child findings only when the original issue cannot be managed as one coherent unit
- a finding may be merged only when multiple findings are shown to be manifestations of the same root issue
- merges, splits, and re-scopes must preserve lineage notes rather than replacing history

Each finding must use one of these statuses:
- `open`
- `in_remediation`
- `pending_evaluation`
- `carried_forward`
- `re_scoped`
- `split`
- `merged`
- `closed`

Status meanings:
- `open`: a finding is active and not yet being remediated
- `in_remediation`: corrective work is in progress
- `pending_evaluation`: remediation is complete enough to evaluate
- `carried_forward`: the finding remains materially the same in a new cycle
- `re_scoped`: the finding remains active but its boundary or interpretation changed without becoming a merge or split case
- `split`: the original finding no longer stands alone and has been replaced by child findings with preserved lineage
- `merged`: the finding no longer stands alone because it has been absorbed into a surviving finding representing the shared root issue
- `closed`: closure criteria were met and the finding is no longer active

Each finding must also state closure criteria in advance so that remediation is not judged against an unstated target.

---

## Cycle Packet Structure

Each review/remediation/evaluation/planning/handoff loop should operate on a formal packet with fixed inputs and outputs.

Packet depth scales with consequence. See the Core Granularity Concepts and Decision Points sections for packet depth selection criteria. Even at scaled-back depth, minimum required contents for closure determination must be preserved.

### Review packet
Minimum required contents:
- cycle ID
- review mode
- packet depth declaration
- local work unit granularity statement
- governing documents used
- candidate artifact set
- relevant git references when applicable
- finding records
- evidence notes
- scope statement
- recommended routing assumptions

### Remediation packet
Minimum required contents:
- cycle ID
- target finding IDs
- packet depth declaration
- local work unit granularity statement
- root cause analysis per finding
- implementation or document changes made
- relevant git references when applicable
- impacted surfaces checked
- tests or validation performed
- unresolved risks
- self-assessed readiness for evaluation

### Evaluation packet
Minimum required contents:
- cycle ID
- evaluated finding IDs
- packet depth declaration
- local work unit granularity statement
- closure determination per finding
- evidence for closure or non-closure
- relevant git references when applicable
- downstream issues identified
- document revision recommendation if needed
- next routing recommendation

### Planning packet
Minimum required contents:
- cycle ID
- input evaluation packet reference
- packet depth declaration
- routing decision
- rationale for the routing decision
- active findings for the next cycle
- transformed findings with successor lineage when applicable
- findings closed in this cycle
- findings deferred with justification
- governing-document changes required before the next cycle
- declared starting scope for the next cycle
- next-cycle local work unit granularity assumption
- handoff granularity decision when applicable
- git workflow implications when applicable

### Handoff packet
Minimum required contents:
- source cycle ID
- source packet references
- handoff target or receiving context
- handoff rationale
- handoff granularity statement
- underlying local work unit granularity reference
- active, transformed, and closed finding references relevant to the receiver
- lineage references to underlying work units
- governing-document references
- relevant git references when applicable
- receiver-facing summary of what requires review, integration, acceptance, or follow-on action

Packets exist to reduce reinterpretation loss between phases. If a phase cannot produce its packet cleanly, that is itself process evidence that the work is not yet well-formed.

When a repository is present, packets should reference the branch, commit set, diff, or pull request context relevant to the cycle. These references are evidence handles, not process authority.

---

## Re-Scope Criteria

Re-scoping should occur only when at least one of the following is true:

- the original finding was framed too narrowly to capture the real defect
- the original finding bundled multiple root causes that should be separated
- evaluation shows that the local fix is correct but the real issue is contract ambiguity
- multiple findings are discovered to share one root cause and should be merged
- the issue boundary changed because review scope widened on justified grounds

Re-scoping must not be used to:
- hide non-closure
- rename churn as progress
- defer uncomfortable architectural work without making that deferral explicit

Every re-scope decision must preserve lineage from the prior finding set to the next one.

---

## Stopping Rule And Closure

Closure is not the absence of the original complaint text.

A finding may be closed only when:
- the root issue is addressed
- no material downstream issue introduced by the remediation remains in the affected area
- documentation and comments are aligned
- test coverage is sufficient for the changed behavior and its predictable regressions
- the implementation is correct and complete relative to the governing specification
- the affected area is unlikely to generate immediate avoidable churn in the next cycle

`split` and `merged` findings are valid terminal transformed states for a cycle when:
- successor lineage is explicit
- active successor findings are tracked in the next cycle or surviving finding set
- no closure claim is made for the transformed parent finding itself

A cycle may stop only when one of the following is true:
- all in-scope findings are closed
- remaining findings are validly transformed into `split` or `merged` states with preserved lineage and successor routing
- remaining items were explicitly re-scoped into a new cycle with preserved identity and rationale
- the governing documents were judged insufficient, and the next required action is document revision rather than further remediation
- remaining open findings are explicitly recorded, low severity, non-blocking relative to the current cycle goal, and their deferral has been explicitly accepted by the human owner

Low-severity follow-on findings may remain open only if:
- they are explicitly recorded
- they are non-blocking relative to the current cycle goal
- their deferral is explicitly accepted by the human owner
- deferral does not falsify any closure claim for the items being closed

Closure must be earned at both levels:
- finding-level closure determines whether a specific item is resolved
- cycle-level closure determines whether the current packet can stop

---

## Document Revision Policy During Convergence

The process should revise the spec or foundation instead of forcing another remediation pass when:
- repeated churn points to unclear or incomplete governing language
- reviewers and remediators are making reasonable but incompatible interpretations
- evaluation cannot determine success because the acceptance basis is unstable
- the implementation repeatedly exposes a missing architectural or behavioral contract

When document revision is triggered:
- the revision itself becomes tracked work
- prior finding IDs remain linked to the document ambiguity that forced revision
- the next cycle must state whether it is validating revised documents, revised implementation, or both

---

## Human And Agent Responsibilities

The process is designed to support delegation, but not all decisions should be automated.

Human-controlled responsibilities:
- approving the governing intent when tradeoffs have meaningful strategic consequences
- accepting explicitly documented low-severity residual risk
- deciding when a document revision materially changes project direction
- adjudicating unresolved conflicts between process goals
- resolving conflicts between agent outputs
- making go/no-go decisions at spike decision points

Agent-delegable responsibilities:
- drafting and revising documents
- implementing against an explicit spec
- performing structured reviews
- producing review, remediation, evaluation, planning, and handoff packets
- tracing lineage, evidence, and closure status when the governing rules are clear
- maintaining coherent git references that support packet traceability in repository-backed work
- selecting and revising local work unit granularity and handoff granularity when the governing rules make the choice explainable
- flagging out-of-scope work discovered during execution or review

If an agent cannot explain the routing, granularity, handoff, or closure rationale in packet form, that decision should not be treated as safely delegated.

### Agent failure modes

**Out-of-scope work:** When an agent produces work outside the declared scope, the out-of-scope rule applies in full: flag and remove the work, then pause and re-scope the affected area and all downstream work before build resumes. This carries the same cost structure as a late spike and is the direct negative feedback for insufficient scope definition upstream.

**Conflicting agent outputs:** When two agents produce outputs that are materially inconsistent — for example, a review and evaluation that disagree on closure status for the same finding — the conflict must be escalated to a human for adjudication. Agent output conflicts are not resolved by agents. A conflict of this kind should also be treated as a signal that the governing documents contain ambiguity sufficient to support incompatible interpretations. The foundation or spec should be inspected for the interpretation gap that permitted the divergence. The conflict is not solely an agent quality problem.

---

## The Convergence Loop

The review -> remediation -> evaluation -> planning -> handoff sequence is not intended as five independent activities. It is a convergence loop.

### Review
Review determines:
- what is wrong
- what is incomplete
- what is misleading
- what is structurally weak
- where the code and docs diverge from the spec
- whether issue framing or scope needs adjustment
- whether any work falls outside the declared scope

### Remediation
Remediation determines:
- why the issue exists
- what the smallest durable fix is
- what blast radius the fix has
- what must be updated in code, tests, docs, comments, and surrounding abstractions
- whether document ambiguity, rather than implementation quality, is the binding problem

### Evaluation
Evaluation determines:
- whether the remediation actually resolved the prior finding
- whether the fix created or exposed downstream issues
- whether documentation and comments are aligned
- whether test coverage is sufficient
- whether the item should be closed, carried forward, re-scoped, merged, split, rerouted into document revision, or prepared for handoff

### Planning
Planning determines:
- whether the current cycle closes
- what the next route is
- what findings remain active or transformed
- what local work unit granularity is appropriate next
- what packet depth is appropriate next
- what handoff granularity is appropriate next, if any
- what governing artifacts must be revised before further implementation work

### Handoff
Handoff determines:
- what the next receiving context must know
- what larger thread must be preserved for external or non-local continuation
- what artifacts and evidence must travel with the package
- what review, integration, acceptance, or follow-on responsibilities now transfer

### Repeat
The loop repeats until closure is earned or the governing docs must be revised.

---

## Likely Failure Zones

The process currently appears most vulnerable in the following areas:

### 1. Downstream effects
A local remediation may appear to fix a finding while:
- leaving dependent callers inconsistent
- introducing special-case logic
- creating architectural drift
- causing adjacent abstractions or tests to become stale

### 2. Documentation drift
Code changes may outpace:
- specs
- foundation decisions
- repo guidance
- comments
- examples
- user-facing docs

### 3. Test insufficiency
Tests may be updated just enough to pass while failing to cover:
- the corrected behavior directly
- edge cases
- regressions
- integration boundaries touched by the change

### 4. Tracking overhead replacing clarity
Formal packets and durable IDs can become ceremony if they are maintained mechanically rather than used to preserve reasoning and routing discipline.

### 5. Granularity mismatch
Work may be chunked too finely for coherent external consumption or too coarsely for truthful local evaluation.

### 6. Handoff under-specification
Cross-team or non-local transfer may appear efficient while silently dropping lineage, receiver expectations, or integration context.

### 7. Document ambiguity mistaken for implementation failure
Repeated review/remediation churn may indicate that the governing documents are under-specified, internally tense, or silent on key points.

### 8. Late spikes
Blocking unknowns that surface during build rather than during foundation or specification work impose mandatory pauses on all downstream work. The process is vulnerable to teams treating late spikes as normal rather than as evidence of insufficient upfront definition.

### 9. Tool state treated as process authority
Teams under pressure may allow tool state — sprint boards, issue tracker status, PR merge — to substitute for earned closure and explicit routing decisions. This failure mode is silent and tends to compound across cycles.

### 10. Packet depth set too low
Scaled-back packets applied to work that carries non-trivial risk or high business value may produce insufficient evidence for closure determination. This failure mode may not become visible until a downstream cycle inherits an under-documented prior state.

---

## Closed Decisions

### Living documents are mandatory
**Decision:** Foundation, specification, and related process documents are treated as living documents rather than frozen artifacts.

**Reasoning:** The process depends on iterative clarification and correction. Freezing documents too early would force later work to drift away from them or treat them as ceremonial rather than authoritative.

### Specification is the implementation authority
**Decision:** The spec, not the codebase, is the authoritative implementation contract.

**Reasoning:** Without an authoritative spec, review and remediation become relative to current implementation rather than intended implementation, which weakens convergence and invites drift.

### Review-remediation-evaluation-planning-handoff is a convergence loop
**Decision:** These steps are treated as a repeated control loop rather than isolated phases.

**Reasoning:** The goal is not merely to find and fix defects, but to reduce uncertainty until closure is earned and churn declines.

### Closure must be earned
**Decision:** A finding is not closed merely because a visible change was made.

**Reasoning:** Apparent fixes often leave downstream effects, stale documentation, or weak tests. Closure must reflect actual stability under subsequent review pressure.

### Durable finding identity is mandatory
**Decision:** Findings must retain stable IDs and lineage across cycles.

**Reasoning:** Without stable identity, the process cannot reliably distinguish progress, churn, re-scoping, transformation, and drift.

### Packetized cycles are mandatory
**Decision:** Review, remediation, evaluation, planning, and handoff each operate on explicit packets with fixed minimum structure.

**Reasoning:** Without packet structure, phase transitions depend too heavily on interpretation and memory, which weakens auditability and convergence.

### Human risk acceptance does not override closure discipline
**Decision:** Human acceptance of residual risk is allowed only for explicitly documented low-severity, non-blocking items.

**Reasoning:** The process is explicitly designed to avoid silent override behavior and false closure claims.

### Git is a supporting substrate, not a governing authority
**Decision:** In software engineering contexts, `git` is the default mechanism for versioned state tracking and change evidence, but it does not determine process semantics, routing, or closure.

**Reasoning:** Repository history is valuable evidence, but commits, branches, and pull requests are not substitutes for finding identity, packet structure, root-cause analysis, or earned closure.

### Granularity is dynamic and role-relative
**Decision:** Local work unit granularity, review scope, and handoff granularity may differ from one another and should be chosen relative to the cognitive and coordination needs of the current phase and participants.

**Reasoning:** Local execution, evaluation, and cross-team handoff do not always benefit from the same packaging. The process must preserve coherence without forcing one fixed unit size across all contexts.

### Handoff packetization is proportional
**Decision:** A handoff packet is required for external handoff and optional for other non-local handoff when continuity risk justifies it.

**Reasoning:** Some transfer boundaries require formal packaging to preserve context and expectations, but mandatory packetization for every minor non-local transfer would add avoidable ceremony.

### Transformed findings may terminate a cycle without being closed
**Decision:** `split` and `merged` findings are valid terminal transformed states when successor lineage and routing are explicit.

**Reasoning:** A transformed parent finding is not resolved in the same way as a closed finding, but the cycle must still be able to terminate cleanly when the issue has been truthfully redistributed into successor structure.

### Packet depth scales with consequence
**Decision:** Packet depth is calibrated to the risk and business value of the work, not fixed to process position. Full packet depth is required when work carries non-trivial risk or sufficient business value. Scaled-back depth is permitted only when decisions are already made, the change is reversible, and mistakes are cheap to recover from.

**Reasoning:** Uniform full-depth packets for all work sizes adds avoidable ceremony to low-consequence work. Uniform scaled-back packets for all work risks under-documenting high-consequence decisions. The right packet depth is the one that is honest about the stakes.

### Spikes are diagnostic, not a standalone phase
**Decision:** A spike is a time-boxed investigation triggered when a blocking unknown prevents scoping or design from proceeding. It is not a process phase. It is a signal that an upstream governing document requires revision.

**Reasoning:** Treating spikes as a normal phase would normalize late discovery of blocking unknowns. The process must treat spikes as a cost with negative feedback pressure to front-load unknowns into foundation and specification work.

### Late spikes carry mandatory downstream pause
**Decision:** A spike triggered during build requires a mandatory pause on all related and downstream work until the spike resolves and governing documents are revised. Downstream work must not continue in parallel with an open spike.

**Reasoning:** Continuing downstream work while a blocking unknown is open risks implementing against a spec that will change, compounding rework and churn. The pause cost is intentional and attributable to insufficient upfront definition.

### Tooling is out of scope for process definition
**Decision:** Process artifacts are the authoritative record. Tool state does not determine closure, routing, or finding identity. The process is tool-agnostic by design.

**Reasoning:** Tools optimize for communication and visibility, not for closure discipline or lineage preservation. Coupling the process to any specific tool would degrade it to whatever that tool can model and create fragility across tool migrations.

### Brownfield entry uses the same process entry point as greenfield
**Decision:** Brownfield work begins at intent formation, seeded by the specific motivation driving the work. No special onboarding phase is required. The existing codebase is the environment the work occurs within, not a prerequisite artifact to document before work begins.

**Reasoning:** Brownfield work is always motivated by something specific. That motivation is sufficient to seed a foundation document. Treating the entire existing codebase as a prerequisite to document would make the process unusable in legacy environments.

### Agent output conflicts require human adjudication
**Decision:** When agents produce materially conflicting outputs, the conflict is escalated to a human. Agents do not resolve conflicts between agent outputs. Conflicts are also treated as signals of governing document ambiguity.

**Reasoning:** Agent conflicts often reflect genuine ambiguity in the governing documents rather than agent error alone. Human adjudication forces explicit resolution and surfaces the interpretation gap that must be closed in the governing documents.

---

## Preliminary Process Success Criteria

A successful use of this process likely has the following properties:

- the implemented system matches the current specification
- the specification remains aligned with the clarified intent in the foundation
- architectural boundaries remain coherent under review pressure
- documentation and comments remain truthful
- test coverage remains aligned with behavior
- repeated cycles decrease rather than proliferate
- issue history remains traceable across cycles
- routing decisions are explainable from packet evidence
- granularity choices are explainable from coherence, evaluability, and coordination constraints
- packet depth choices are explainable from risk and business value
- handoff packaging preserves receiver comprehension without falsifying underlying local work structure
- spikes are rare and occur early rather than during build
- tool state is never treated as the basis for a closure or routing decision
- when churn persists, the process correctly identifies whether the problem lies in code, spec, foundation, or issue framing

---

## Notes

This document is intentionally pre-spec.  
It should remain a place where process ideas, concerns, invariants, and operating assumptions can be revised before they are formalized into an authoritative process specification.

The process itself should be subjected to the same discipline it imposes:
- clarify intent
- define contract
- review against that contract
- remediate at the root
- evaluate for closure
- plan the next route explicitly
- hand off explicitly when needed
- repeat until the process documentation itself converges
