# Process Specification v2

> **Governing document:** Process Foundation Document v6
> **Status:** Initial draft
> **Purpose:** This document is the formal implementation contract for the documentation-driven development and convergence process. It defines what must be done, how the process must behave, and what counts as correct, complete, and acceptable at every phase.

---

## 1. Preamble

This specification is derived from Process Foundation Document v6 and governs all work conducted under the documentation-driven development and convergence process.

The foundation document is the upstream intent record. This specification is its downstream behavioral contract. Where the foundation records philosophy, constraints, and rationale, this specification records requirements. Where the foundation describes concepts, this specification defines what must be produced and how it must behave.

This specification is a living document. It MUST be revised when:

- repeated convergence cycles expose ambiguity or incompleteness in its requirements
- the foundation document is revised in ways that alter the behavioral contract
- acceptance criteria are found to be unstated or misleading

When this specification is revised, the revision MUST be treated as tracked work with an explicit reason, linked to any finding or foundation change that triggered it.

The most recent version of this specification supersedes all prior versions.

---

## 2. Normative Terminology

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHOULD**, **SHOULD NOT**, and **MAY** in this document are to be interpreted as follows:

- **MUST** / **REQUIRED**: The requirement is absolute. Conforming process execution must satisfy it without exception unless an explicit exception is documented and accepted by a human owner.
- **MUST NOT**: The behavior is absolutely prohibited.
- **SHOULD**: The requirement represents a strong preference. Deviation is permitted only when there is a documented, justified reason and the deviation does not undermine the intent the requirement protects.
- **SHOULD NOT**: The behavior is strongly discouraged. Deviation requires the same justification standard as SHOULD.
- **MAY**: The behavior is permitted but not required.

Normative requirements apply to all phases, participants, and artifacts governed by this specification unless explicitly scoped otherwise.

---

## 3. Scope and Applicability

### 3.1 What This Specification Governs

This specification governs the documentation-driven development and convergence process. It applies to any work whose governing intent is captured in a foundation document and whose implementation is governed by a specification derived from that foundation.

### 3.2 Greenfield Applicability

In greenfield contexts, the process MUST begin at intent formation (Phase 1). No phase MAY be skipped.

### 3.3 Brownfield Applicability

In brownfield contexts, the process MUST begin at intent formation (Phase 1), seeded by the specific motivation driving the work — a feature, rework, migration, compliance requirement, or other explicit driver.

The existing codebase is the environment in which the work occurs. It MUST NOT be treated as a prerequisite artifact that must be fully documented before work begins. Coupling risks, legacy behavior, and discovered findings surface through the process as constraints.

The scope of brownfield work is defined by what the motivating driver touches. It MUST NOT be expanded to encompass the full existing codebase unless the motivating driver explicitly requires it.

#### 3.3.1 Brownfield Scope Drift Prevention

In brownfield contexts, each cycle's scope declaration MUST reference the original motivating driver and MUST justify any scope change relative to that driver. Scope changes that cannot be justified by direct reference to the motivating driver MUST be treated as evidence that the motivating driver itself needs to be revised — which triggers a document revision per Section 14.

> **Advisory note:** When gradual scope drift is a commonly observed failure mode in a team, group, or organization executing this process, cumulative scope tracking across cycles — such as a running log of scope changes with their justifications and the cumulative distance from the original motivating driver — SHOULD be adopted as an organizational practice to provide early warning of drift.

### 3.4 Tool-Agnostic Stance

This process is tool-agnostic by design. The process MUST NOT be coupled to any specific tool, platform, or workflow system.

Tools such as issue trackers, sprint boards, or project management platforms MAY be used for communication and visibility. Tool state MUST NOT be treated as authoritative over process artifact state. If tool state conflicts with process artifact state, process artifact state is authoritative.

In software engineering contexts, `git` is the default mechanism for versioned state tracking and change evidence. Git history MUST NOT substitute for packet structure, finding identity, or closure discipline. Git references in packets are evidence handles, not process authority.

---

## 4. Process Overview

> This section is non-normative. It provides orientation. Normative requirements are in the sections that follow.

The process has eight phases:

1. **Intent Formation** — raw ideas, constraints, invariants, tradeoffs, and non-goals are distilled into a foundation document.
2. **Specification Formation** — the foundation document is used to derive a formal implementation specification.
3. **Build Execution** — implementation agents build against the specification.
4. **Review** — a review agent evaluates the implementation against the governing specification and quality standards.
5. **Remediation** — a remediation agent resolves review findings at the root with minimal durable change.
6. **Evaluation** — an evaluation agent assesses the remediation and determines what is resolved, open, or requires follow-on work.
7. **Cycle Planning** — a planning step determines the next route: close, continue, re-scope, revise governing documents, or hand off.
8. **Handoff** — when work moves to another receiving context, a handoff step packages the cycle outcome.

The high-level operational flow is:

**clarify → specify → build → review → remediate → evaluate → plan → hand off when needed → repeat as needed**

Phases 4–8 form the convergence loop, which repeats until closure is earned or governing documents must be revised.

Each phase exists to reduce a different kind of uncertainty:

- Phase 1 reduces uncertainty about intent.
- Phase 2 reduces uncertainty about required behavior.
- Phase 3 reduces uncertainty about implementability.
- Phase 4 reduces uncertainty about defects and mismatches.
- Phase 5 reduces uncertainty about corrective action.
- Phase 6 reduces uncertainty about closure status.
- Phase 7 reduces uncertainty about what to do next.
- Phase 8 reduces uncertainty for the next receiving context.

No phase is complete unless it produces explicit artifacts that the next phase can consume without reinterpretation.

A spike MAY be triggered during Phase 2 or Phase 3 when a specific blocking unknown prevents scoping or design from proceeding. A spike is not a phase — it is a diagnostic mechanism. See Section 6.

---

## 5. Phase Requirements

### 5.1 Phase 1: Intent Formation

#### Inputs

The following inputs MUST be available or discoverable before or during intent formation:

- The motivating driver for the work (idea, problem statement, feature request, compliance requirement, or other explicit motivation).
- Any known constraints, invariants, or non-goals.

#### Required Actions

- Participants MUST explore and distill the motivating driver into explicit intent.
- Participants MUST record key constraints, invariants, and non-goals.
- Participants MUST record major tradeoffs that have been accepted or considered.
- Participants SHOULD identify and record high-level design ambiguities that, if left unresolved, would invalidate specification work.
- Participants MUST produce a foundation document as the output of this phase.

#### Required Output

- Foundation document conforming to the artifact requirements in Section 7.1.

#### Readiness Gate — Advancing to Phase 2

The foundation is ready to feed the specification when ALL of the following hold:

- Core intent is stable and explicit.
- Major constraints are explicit.
- Key non-goals are explicit.
- Major tradeoffs are recorded.
- No unresolved high-level design ambiguity remains that would invalidate specification work.

The process MUST NOT advance to Phase 2 until this gate is satisfied.

---

### 5.2 Phase 2: Specification Formation

#### Inputs

The following inputs MUST be available before specification formation begins:

- A foundation document that has passed the Phase 1 readiness gate.

#### Required Actions

- Participants MUST derive a formal specification from the foundation document.
- The specification MUST be iterated until it is precise enough to govern implementation and review.
- Participants MUST ensure the specification answers: what exactly must be built, how must it behave, and what counts as correct, complete, and acceptable.
- If a blocking unknown prevents specification from proceeding, participants MUST trigger a spike (see Section 6) rather than proceeding with an underspecified contract.

#### Required Output

- Specification document conforming to the artifact requirements in Section 7.2.

#### Readiness Gate — Advancing to Phase 3

The specification is ready to feed implementation when ALL of the following hold:

- Required behavior is explicit.
- Architectural boundaries are explicit.
- The error model is defined.
- Important edge cases are covered.
- Acceptance criteria are concrete enough to review against.

The process MUST NOT advance to Phase 3 until this gate is satisfied.

---

### 5.3 Phase 3: Build Execution

#### Inputs

The following inputs MUST be available before build execution begins:

- A specification that has passed the Phase 2 readiness gate.
- Any repository guidance that governs implementation practices.

#### Required Actions

- Implementation agents MUST build against the specification, not against implicit inference or prior implementation patterns alone.
- Implementation agents MUST NOT treat the codebase as authoritative over the specification.
- If a blocking unknown prevents implementation from proceeding, participants MUST trigger a spike (see Section 6) rather than proceeding against an underspecified contract.
- Out-of-scope work discovered during build execution MUST be flagged and removed. The affected area and all downstream work MUST be paused and re-scoped before build resumes.

#### Required Output

- Build artifacts that constitute a meaningful candidate against the current specification.

#### Readiness Gate — Advancing to Phase 4

The implementation is ready for review when it is a meaningful candidate against the current specification rather than an incomplete sketch.

The process MUST NOT advance to Phase 4 until this gate is satisfied.

---

### 5.4 Phase 4: Review

#### Inputs

The following inputs MUST be available before review begins:

- Build artifacts that have passed the Phase 3 readiness gate.
- The governing specification.
- A declared review mode (`broad` or `delta` — see Section 10.2).
- A declared packet depth (see Section 8.2).
- A declared local work unit granularity (see Section 10.1).

#### Required Actions

- The reviewing agent MUST evaluate the implementation against the governing specification.
- The reviewing agent MUST assess architecture, correctness, completeness, coherence, and documentation accuracy.
- The reviewing agent MUST operate within the declared review scope.
- The reviewing agent MUST NOT silently widen scope without justification and documentation.
- The reviewing agent MUST flag any work that falls outside the declared scope rather than reviewing it silently.
- The reviewing agent MUST produce a finding record for each identified issue, conforming to Section 9.
- The reviewing agent MUST produce a review packet conforming to the template in Section 8.3.

#### Required Output

- Review packet (see Section 8.3).
- One finding record per identified issue (see Section 9).

#### Readiness Gate — Advancing to Phase 5

The review packet is ready to feed remediation when it contains all required fields and finding records are complete enough that remediation can proceed without reinterpretation.

---

### 5.5 Phase 5: Remediation

#### Inputs

The following inputs MUST be available before remediation begins:

- A review packet from Phase 4.
- The finding records being addressed.
- The governing specification.
- A declared packet depth.
- A declared local work unit granularity.

#### Required Actions

- The remediating agent MUST target the root cause of each finding, not only the visible symptom.
- The remediating agent MUST produce a root cause analysis per finding.
- The remediating agent MUST assess and document the blast radius of each change.
- The remediating agent MUST update code, tests, documentation, comments, and surrounding abstractions as required by each finding.
- The remediating agent MUST NOT claim closure for a finding based solely on a code change having occurred.
- If document ambiguity is identified as the binding problem, the remediating agent MUST flag this for document revision consideration rather than treating implementation as the only issue.
- The remediating agent MUST produce a remediation packet conforming to the template in Section 8.4.

#### Remediation Sequencing

When multiple findings are being addressed in a single remediation pass, the remediating agent MUST declare a sequencing rationale before remediation begins. The rationale MUST explain why findings are being addressed in the chosen order.

The remediating agent SHOULD address findings in severity-descending order: `critical` → `major` → `minor` → `informational`.

Deviation from severity-descending order is permitted when justified. Valid justifications include:

- Two or more findings share a root cause and addressing them together is more efficient regardless of individual severity.
- A lower-severity finding must be resolved first because a higher-severity finding depends on its resolution.
- Addressing a group of related findings in a coherent sequence produces a more intelligible remediation story than strict severity ordering.

The sequencing rationale and any deviation justifications MUST be recorded in the remediation packet.

#### Required Output

- Remediation packet (see Section 8.4).

#### Readiness Gate — Advancing to Phase 6

The remediation packet is ready for evaluation when it contains all required fields and the remediating agent has self-assessed readiness for evaluation.

---

### 5.6 Phase 6: Evaluation

#### Inputs

The following inputs MUST be available before evaluation begins:

- The remediation packet from Phase 5.
- The review packet from Phase 4 (the most recent prior review).
- The finding records being evaluated.
- The governing specification.
- A declared packet depth.
- A declared local work unit granularity.

#### Required Actions

- The evaluating agent MUST determine closure status for each finding based on the criteria in Section 12.1.
- The evaluating agent MUST identify downstream issues introduced or exposed by the remediation.
- The evaluating agent MUST assess whether documentation and comments are aligned with the changed behavior.
- The evaluating agent MUST assess whether test coverage is sufficient for the changed behavior and its predictable regressions.
- The evaluating agent MUST NOT close a finding based solely on the presence of a code change or passing tests.
- The evaluating agent MUST produce an evaluation packet conforming to the template in Section 8.5.
- If evaluation cannot determine success because the acceptance basis is unstated or conflicted, the evaluating agent MUST flag this for document revision consideration.

#### Required Output

- Evaluation packet (see Section 8.5).
- Updated closure status on each evaluated finding record.

#### Readiness Gate — Advancing to Phase 7

The evaluation packet is ready to feed cycle planning when it contains all required fields and a clear closure determination per finding.

---

### 5.7 Phase 7: Cycle Planning

#### Inputs

The following inputs MUST be available before cycle planning begins:

- The evaluation packet from Phase 6.
- All active finding records for the current cycle.
- The governing specification and foundation document.

#### Required Actions

- The planning agent MUST select exactly one routing decision from the following options:
  - `close` — all in-scope findings are closed or validly transformed.
  - `continue_remediation` — implementation gaps remain that warrant another convergence pass.
  - `re_scope` — the real issue is broader or differently shaped than originally framed.
  - `revise_governing_documents` — repeated churn indicates ambiguity, tension, or incompleteness in the governing documents.
  - `prepare_handoff` — the next receiving context is meaningfully non-local.
- The planning agent MUST document the rationale for the routing decision.
- The planning agent MUST explicitly account for all active findings — closed, carried forward, re-scoped, transformed, or deferred with justification.
- The planning agent MUST declare the starting scope and granularity assumptions for the next cycle.
- The planning agent MUST produce a planning packet conforming to the template in Section 8.6.

#### Required Output

- Planning packet (see Section 8.6).

#### Post-Planning

If the routing decision is `close`, no further convergence passes are required for in-scope findings.

If the routing decision is `revise_governing_documents`, the revision MUST be treated as tracked work and MUST be completed before the next implementation cycle begins.

If the routing decision is `prepare_handoff`, Phase 8 MUST be executed before the cycle terminates.

---

### 5.8 Phase 8: Handoff

#### Inputs

The following inputs MUST be available before handoff begins:

- A planning packet that includes a `prepare_handoff` routing decision.
- All relevant cycle artifacts (review, remediation, evaluation, and planning packets; finding records; governing documents).

#### When Required

A handoff packet is REQUIRED when transferring work to another team, owner, or materially separate receiving context.

A handoff packet is OPTIONAL but allowed for any other non-local handoff when continuity risk, async delay, ownership separation, or auditability needs justify formal packaging.

#### Required Actions

- The handoff agent MUST package the cycle outcome at a granularity that preserves the larger thread well enough for the receiver to review, integrate, or accept it without excessive reconstruction cost.
- The handoff agent MUST declare the handoff granularity and MUST reference the underlying local work unit granularity.
- The handoff agent MUST preserve lineage to underlying work units.
- The handoff agent MUST preserve finding identity and truthful closure and non-closure claims.
- The handoff agent MUST explicitly state what review, integration, acceptance, or follow-on work the receiver is expected to perform.
- The handoff agent MUST produce a handoff packet conforming to the template in Section 8.7.

#### Required Output

- Handoff packet (see Section 8.7).

#### Receiver Acceptance Gate

When a handoff packet is produced, the receiving context MUST confirm that the handoff is sufficient before accepting it.

A handoff is sufficient when ALL of the following hold:

- All referenced finding records are accessible and carry the expected status and version.
- All governing document references are resolvable to the correct versions.
- The receiver-facing summary is actionable — the receiver can determine what to do next without consulting the sender.
- Lineage to underlying work units is intact and traceable.
- The handoff granularity is appropriate for the receiver's coordination context.

If the handoff fails the receiver acceptance gate:

- The receiver MUST document which sufficiency criteria were not met.
- The sender MUST remediate the handoff packet — not the underlying work — until the gate is passed.
- The handoff remediation is a packaging correction, not a new convergence cycle. It does not require a new cycle ID.

---

## 6. Spike Requirements

A spike is a time-boxed investigation triggered when a specific blocking unknown prevents scoping or design from proceeding. A spike is not a phase — it is a diagnostic mechanism that signals that an upstream governing document requires revision.

### 6.1 Trigger Criteria

A spike MUST be triggered when BOTH of the following hold:

- A specific blocking unknown prevents scoping or design from proceeding.
- The unknown cannot be resolved by further iteration on the existing governing documents alone.

A spike MUST NOT be triggered when:

- The blocking unknown results from insufficient effort on foundation or specification work.
- The intent is to defer scoping work rather than resolve a genuine unknown.

### 6.2 Required Inputs

A spike MUST declare, at minimum:

- A clearly stated blocking unknown.
- A declared time-box.
- A reference to the governing document whose insufficiency triggered the spike.

### 6.3 Required Outputs

A spike MUST produce exactly one of the following outcomes:

1. **Unblocked** — the investigation produced enough clarity to proceed. The governing document MUST be revised before work resumes.
2. **Blocked** — work cannot continue. The reason and implications MUST be explicitly documented.
3. **Decision point** — continuation is possible but not automatic. A human go/no-go decision with explicit justification is REQUIRED before work resumes.

### 6.4 Mandatory Downstream Pause

A spike triggered during Phase 3 (Build Execution) MUST trigger a mandatory pause on all work related to or downstream of the affected area.

This pause MUST persist until the spike resolves and the governing documents are revised.

Downstream work MUST NOT continue in parallel with an open spike.

### 6.5 Front-Loading Requirement

Spikes SHOULD be front-loaded into the earliest possible stage of the process. A spike during Phase 2 is preferred over a spike during Phase 3.

A spike triggered during Phase 3 SHOULD be treated as evidence of insufficient definition in the foundation or specification and SHOULD prompt review of those documents regardless of the spike outcome.

---

## 7. Artifact Requirements

### 7.1 Foundation Document

The foundation document MUST:

- Capture explicit intent.
- Preserve key constraints.
- Record the process philosophy and non-goals.
- Record major tradeoffs that have been accepted.
- Record closed decisions with rationale.
- Provide the upstream source from which the specification is derived.

The foundation document MUST be treated as a living document. It MAY be revised when new constraints or tradeoffs emerge, intent requires clarification, closed decisions require re-examination, or the specification or convergence cycles expose ambiguity or incompleteness.

### 7.2 Specification

The specification MUST:

- Define the implementation contract.
- Provide authoritative behavioral and architectural requirements.
- Define acceptance criteria.
- Define testing expectations.
- Govern implementation and review.

The specification MUST be treated as a living document. It MUST NOT be treated as frozen.

The codebase MUST NOT be treated as authoritative over the specification. When implementation and specification conflict, the conflict MUST be surfaced as a finding rather than resolved by treating the implementation as correct.

### 7.3 Finding Record

Each finding MUST include at minimum:

| Field | Requirement | Notes |
|---|---|---|
| `id` | MUST | Assigned at first explicit statement of the finding. Format: `<DOMAIN>-<AREA>-<NNN>`. Example: `PROC-TRACK-001`. |
| `title` | MUST | Concise, stable description of the issue. |
| `originating_cycle` | MUST | Reference to the cycle in which the finding first appeared. |
| `severity` | MUST | One of the severity values defined in Section 9.2. |
| `governing_source` | MUST | Reference to the specification section, principle, or requirement the finding violates. |
| `affected_area` | MUST | Description of the code, document, or abstraction affected. |
| `status` | MUST | One of the status values defined in Section 9.3. |
| `closure_criteria` | MUST | Stated before remediation begins. |
| `version` | MUST | Monotonic integer version identifier. See Section 9.7. |
| `lineage_notes` | MUST if transformed | Present if the finding was merged, split, or re-scoped. |

Finding records MUST be maintained as governed process artifacts. Tool state MUST NOT be the sole record of a finding.

### 7.4 Git History

In software engineering contexts, `git` is the default version-control substrate for governed artifacts.

Git history MUST be used to support:

- Durable version history for governed artifacts.
- Inspectable diffs for document and implementation changes.
- Evidence handles for packet references.

Git history MUST NOT substitute for:

- Packet structure.
- Finding identity or status.
- Closure decisions.
- Routing rationale.

### 7.5 Document Versioning

Governing documents — foundations and specifications — MUST carry a monotonic integer version identifier (e.g., v1, v2, ... vN). The version number MUST increment by one with each revision.

When a packet references a governing document, the reference MUST include the version identifier so that the reference is pinned to the specific version in effect at the time.

The most recent version of a governing document supersedes all prior versions. Prior versions MUST remain available in version-control history for traceability.

---

## 8. Packet Requirements and Templates

### 8.1 Cycle ID Requirements

Each cycle MUST be assigned a unique, durable cycle ID at the point the cycle begins.

The default cycle ID format is: `<PROJECT>-CYC-<NNN>`

Example: `PROCDEV-CYC-001`

The project component MUST be consistent within a project. The numeric component MUST be unique within a project and MUST NOT be reused, even after a cycle closes.

Cycle IDs MUST survive across all phases and packets within a cycle and MUST remain stable in references from later cycles.

### 8.2 Packet Depth Requirements

Packet depth scales with consequence. There are two packet depth modes: `standard` and `fast-track`.

**Standard depth** is the default and MUST be used unless fast-track eligibility is satisfied.

Standard depth is REQUIRED when at least one of the following holds:

- The work carries non-trivial risk.
- Business value is sufficient that mitigation overhead is justified by the cost of a mistake.
- Multiple findings are being addressed in the cycle.
- Any finding is `critical` or `major` severity.
- The change involves architectural boundaries, public interfaces, or non-reversible state changes.

At standard depth, all fields marked MUST in the packet templates below are required. Fields marked SHOULD are recommended and MUST be present when the work carries non-trivial risk.

**Fast-track depth** is a genuinely reduced-overhead mode for trivial work. See Section 8.2.3 for eligibility criteria and packet requirements.

Packet depth MUST be determinable before a cycle begins. If packet depth cannot be determined, the work is not ready to advance.

Each packet MUST include a `packet_depth` field with value `standard` or `fast-track`.

### 8.2.1 Reconstruction Completeness Requirement

Every cycle MUST produce artifacts explicit enough that a new participant could reconstruct the state of the work without relying on oral history, tool state, or implicit knowledge. This requirement applies at all packet depths, including fast-track.

### 8.2.2 Mid-Cycle Fast-Track Escalation

Any phase participant (reviewer, evaluator, remediator) MAY recommend packet depth escalation from `fast-track` to `standard` when evidence discovered mid-cycle indicates that fast-track eligibility criteria are no longer satisfied.

When packet depth is escalated mid-cycle:

- The escalation MUST be documented in the current packet with the rationale for why fast-track eligibility was invalidated.
- All subsequent packets in the same cycle MUST use standard depth.
- Escalation is one-directional: `standard` to `fast-track` is NOT permitted mid-cycle.

### 8.2.3 Fast-Track Eligibility and Requirements

Fast-track depth is PERMITTED only when ALL of the following hold:

- The cycle addresses exactly one finding.
- The finding is `minor` or `informational` severity.
- The change is fully reversible.
- The change does not affect architectural boundaries, public interfaces, or shared abstractions.
- No meaningful decision points remain — the work is implementation only.
- Mistakes are cheap to recover from in both effort and cost.
- No scope ambiguity exists.

Fast-track eligibility MUST be declared before the cycle begins. The declaration MUST explicitly confirm each eligibility criterion.

**Fast-track packet requirements:**

At fast-track depth, the four standard packets (review, remediation, evaluation, planning) are replaced by a single **fast-track combined packet** conforming to the template in Section 8.8.

The fast-track combined packet preserves the essential content of each phase — finding identity, evidence, closure determination, and routing — in a single document rather than four separate artifacts.

**Fast-track escalation trigger:**

If at any point during a fast-track cycle, a participant discovers that any eligibility criterion is no longer satisfied — including discovery of additional findings, unexpected complexity, scope ambiguity, or non-reversibility — the cycle MUST be escalated to standard depth immediately per Section 8.2.2. Work completed under fast-track rules MUST be repackaged into standard-depth packets before the cycle may proceed.

---

### 8.3 Review Packet Template

| Field | Requirement | Notes |
|---|---|---|
| `cycle_id` | MUST | Unique identifier for this cycle. |
| `packet_depth` | MUST | `standard` or `fast-track`. |
| `review_mode` | MUST | `broad` or `delta`. See Section 10.2. |
| `local_work_unit_granularity` | MUST | Statement of the work unit size and coherence rationale. |
| `governing_documents` | MUST | List of governing documents used, including versions. |
| `candidate_artifact_set` | MUST | Description or reference to the artifacts under review. |
| `git_references` | SHOULD | Branch, commit, diff, or PR references. MUST be present at standard depth. |
| `scope_statement` | MUST | Explicit declaration of what was and was not in scope. |
| `finding_records` | MUST | Reference to each finding record produced. |
| `evidence_notes` | MUST | Evidence observed per finding or per scope area. |
| `scope_widening_justification` | MUST if scope widened | Why widening was necessary, what new boundary was included, whether widening created new findings or recontextualized existing ones. |
| `out_of_scope_flags` | MUST if any | Work found outside declared scope, flagged for removal and re-scoping. |
| `recommended_routing_assumptions` | SHOULD | Non-binding routing signal for cycle planning. |

---

### 8.4 Remediation Packet Template

| Field | Requirement | Notes |
|---|---|---|
| `cycle_id` | MUST | Unique identifier for this cycle. |
| `packet_depth` | MUST | `standard` or `fast-track`. |
| `local_work_unit_granularity` | MUST | Statement of the work unit size and coherence rationale. |
| `target_finding_ids` | MUST | List of finding IDs being addressed. |
| `sequencing_rationale` | MUST | Declared order in which findings are addressed and the reason for that order. If only one finding is present, state that explicitly. If deviation from severity-descending order was used, the deviation justification MUST be included here. |
| `root_cause_analysis` | MUST | Per-finding root cause analysis. Must address why the issue exists, not only what changed. |
| `changes_made` | MUST | Description of implementation or document changes made, per finding. |
| `git_references` | SHOULD | Branch, commit, diff, or PR references. MUST be present at standard depth. |
| `impacted_surfaces_checked` | MUST | Callers, dependents, adjacent abstractions, or documentation surfaces inspected. |
| `tests_or_validation_performed` | MUST | Tests run or validation performed. |
| `unresolved_risks` | MUST | Risks that remain after remediation. Empty if none. |
| `document_ambiguity_flags` | MUST if identified | Governing document ambiguity found to be the binding problem. |
| `self_assessed_readiness` | MUST | Remediating agent's assessment of readiness for evaluation. |

---

### 8.5 Evaluation Packet Template

| Field | Requirement | Notes |
|---|---|---|
| `cycle_id` | MUST | Unique identifier for this cycle. |
| `packet_depth` | MUST | `standard` or `fast-track`. |
| `local_work_unit_granularity` | MUST | Statement of the work unit size and coherence rationale. |
| `evaluated_finding_ids` | MUST | List of finding IDs evaluated in this packet. |
| `closure_determination` | MUST | Per-finding post-evaluation status. One of: `closed`, `open` (remediation insufficient, continuing in current cycle), `carried_forward` (remediation insufficient or unchanged, entering new cycle), `re_scoped`, `split`, `merged`. Not all outcomes are closure — this field records the evaluator's status determination for each finding. |
| `evidence_for_closure_or_non_closure` | MUST | Per-finding evidence supporting the closure determination. |
| `git_references` | SHOULD | Branch, commit, diff, or PR references. MUST be present at standard depth. |
| `downstream_issues_identified` | MUST | New findings introduced or exposed by the remediation. Empty if none. |
| `documentation_alignment_assessment` | MUST | Whether documentation and comments are aligned with changed behavior. |
| `test_coverage_assessment` | MUST | Whether test coverage is sufficient for changed behavior and its predictable regressions. |
| `document_revision_recommendation` | MUST if applicable | Recommendation to revise specification or foundation, with rationale. |
| `next_routing_recommendation` | MUST | Recommended routing decision for cycle planning. |

---

### 8.6 Planning Packet Template

| Field | Requirement | Notes |
|---|---|---|
| `cycle_id` | MUST | Unique identifier for this cycle. |
| `packet_depth` | MUST | `standard` or `fast-track`. |
| `input_evaluation_packet_reference` | MUST | Reference to the evaluation packet consumed. |
| `routing_decision` | MUST | One of: `close`, `continue_remediation`, `re_scope`, `revise_governing_documents`, `prepare_handoff`. |
| `routing_rationale` | MUST | Explicit rationale for the routing decision. |
| `active_findings_for_next_cycle` | MUST | Finding IDs and statuses carried forward. |
| `transformed_findings` | MUST if applicable | Finding IDs with successor lineage for `split` or `merged` states. |
| `closed_findings` | MUST | Finding IDs closed in this cycle. |
| `deferred_findings` | MUST if applicable | Finding IDs deferred, with justification and human acceptance confirmation. |
| `governing_document_changes_required` | MUST | Governing document changes required before the next cycle. Empty if none. |
| `next_cycle_starting_scope` | MUST | Declared starting scope for the next cycle. |
| `next_cycle_granularity_assumption` | MUST | Declared local work unit granularity for the next cycle. |
| `next_cycle_packet_depth_assumption` | MUST | Declared packet depth for the next cycle. |
| `handoff_granularity_decision` | MUST if handoff | Declared handoff granularity when routing decision is `prepare_handoff`. |
| `git_workflow_implications` | SHOULD | Branch, merge, PR, or tagging implications relevant to cycle end. |

---

### 8.7 Handoff Packet Template

| Field | Requirement | Notes |
|---|---|---|
| `source_cycle_id` | MUST | The cycle from which this handoff originates. |
| `source_packet_references` | MUST | References to the review, remediation, evaluation, and planning packets. |
| `handoff_target` | MUST | Description of the receiving team, owner, or context. |
| `handoff_rationale` | MUST | Why the handoff is occurring at this point. |
| `handoff_granularity_statement` | MUST | The granularity at which this handoff is packaged. |
| `underlying_local_work_unit_granularity_reference` | MUST | Reference to the local work unit granularity used during the source cycle. |
| `finding_references` | MUST | Active, transformed, and closed finding references relevant to the receiver. |
| `lineage_references` | MUST | Explicit lineage links to underlying work units. |
| `governing_document_references` | MUST | References to the current foundation and specification documents. |
| `git_references` | SHOULD | Branch, commit, diff, or PR references. MUST be present at standard depth. |
| `receiver_facing_summary` | MUST | Summary of what the receiver must review, integrate, accept, or act on next. |

---

### 8.8 Fast-Track Combined Packet Template

This template replaces the four standard packets (review, remediation, evaluation, planning) when a cycle is executed at fast-track depth per Section 8.2.3.

| Field | Requirement | Notes |
|---|---|---|
| `cycle_id` | MUST | Unique identifier for this cycle. |
| `packet_depth` | MUST | `fast-track`. |
| `fast_track_eligibility_confirmation` | MUST | Explicit confirmation that each eligibility criterion in Section 8.2.3 was satisfied at cycle start. |
| `governing_documents` | MUST | List of governing documents used, including versions. |
| `target_finding_id` | MUST | The single finding ID being addressed. |
| `finding_severity` | MUST | Severity of the target finding. Must be `minor` or `informational`. |
| `scope_statement` | MUST | What was and was not in scope. |
| `review_summary` | MUST | Brief assessment of the issue against the governing specification. |
| `root_cause_summary` | MUST | Brief root cause analysis. |
| `changes_made` | MUST | Description of implementation or document changes made. |
| `git_references` | SHOULD | Branch, commit, diff, or PR references. |
| `tests_or_validation_performed` | MUST | Tests run or validation performed. |
| `closure_determination` | MUST | `closed` or `open`. If `open`, the cycle MUST be escalated to standard depth. |
| `evidence_for_closure` | MUST | Evidence supporting the closure determination. |
| `routing_decision` | MUST | One of: `close` or `continue_remediation`. If `continue_remediation`, the next cycle MUST use standard depth. |

---

## 9. Finding Lifecycle Requirements

### 9.1 ID Assignment

Each finding MUST be assigned a unique, durable ID at the point it first becomes explicit.

The default ID format is: `<DOMAIN>-<AREA>-<NNN>`

Example: `PROC-TRACK-001`

The domain and area components MUST be consistent within a project. The numeric component MUST be unique within a domain-area pair and MUST NOT be reused, even after a finding is closed.

IDs MUST survive across all cycles regardless of wording changes, scope adjustments, or ownership transfers.

### 9.2 Severity Vocabulary

Each finding MUST declare exactly one of the following severity levels:

| Severity | Meaning |
|---|---|
| `critical` | Blocks closure. The defect or gap is severe enough that the affected area cannot be considered safe, correct, or complete. Immediate remediation is REQUIRED. |
| `major` | Materially undermines correctness, coherence, or completeness. Remediation is REQUIRED before closure but MAY be sequenced. |
| `minor` | A real issue that does not block closure on its own. SHOULD be remediated but MAY be deferred with explicit human acceptance per the deferral rules in Section 12.3. |
| `informational` | An observation, suggestion, or style concern. Does not require remediation. MAY inform future work. |

Severity drives packet depth decisions, deferral eligibility, and routing. "Low-severity" in this specification refers to findings with `minor` or `informational` severity.

### 9.3 Status Vocabulary

Each finding MUST carry exactly one of the following statuses at any given point:

| Status | Meaning |
|---|---|
| `open` | The finding is active and not yet being remediated, or has returned to active status after evaluation determined that remediation was insufficient. |
| `in_remediation` | Corrective work is in progress. |
| `pending_evaluation` | Remediation is complete enough to evaluate. |
| `carried_forward` | The finding remains materially the same in a new cycle, or remediation was attempted but judged insufficient and the finding passes to a new cycle. |
| `re_scoped` | The finding remains active but its boundary or interpretation changed without becoming a merge or split case. |
| `split` | The original finding no longer stands alone. It has been replaced by child findings with preserved lineage. |
| `merged` | The finding no longer stands alone. It has been absorbed into a surviving finding representing the shared root issue. |
| `closed` | Closure criteria were met and the finding is no longer active. |

### 9.4 Status Transition Rules

- A finding MUST begin in `open` status.
- A finding MUST transition to `in_remediation` when corrective work begins.
- A finding MUST transition to `pending_evaluation` when remediation is complete enough to evaluate.
- A finding MUST transition to `closed` only when all closure criteria in Section 12.1 are satisfied.
- A finding in `pending_evaluation` whose remediation is judged insufficient by evaluation MUST transition to `open` if remediation continues within the current cycle, or `carried_forward` if the finding passes to a new cycle.
- A finding MAY transition to `carried_forward` when it passes to a new cycle without material change.
- A finding MAY transition to `re_scoped` when its boundary or interpretation changes without producing a split or merge.
- A finding MAY be `split` into child findings. The parent finding MUST NOT be marked `closed`. Child findings MUST be assigned new IDs with lineage notes referencing the parent ID.
- A finding MAY be `merged` into a surviving finding. The absorbed finding MUST NOT be marked `closed`. The surviving finding MUST carry a lineage note referencing the absorbed finding IDs.
- `split` and `merged` are terminal transformed states for a cycle. They are NOT closure states.

### 9.5 Pre-Remediation Closure Criteria Requirement

Closure criteria MUST be stated before remediation begins on a finding. Remediation MUST NOT be judged against an unstated target.

### 9.6 Re-Scope Rules

Re-scoping a finding is PERMITTED only when at least one of the following holds:

- The original finding was framed too narrowly to capture the real defect.
- The original finding bundled multiple root causes that require separation.
- Evaluation shows the local fix is correct but the real issue is contract ambiguity.
- Multiple findings are discovered to share one root cause and should be merged.
- The issue boundary changed because review scope widened on justified grounds.

Re-scoping MUST NOT be used to:

- Hide non-closure.
- Rename churn as progress.
- Defer uncomfortable architectural work without making that deferral explicit.

Every re-scope decision MUST preserve explicit lineage from the prior finding set to the next one.

### 9.7 Finding Record Versioning

Each finding record MUST carry a monotonic integer version identifier (e.g., v1, v2, ... vN). The version number MUST start at v1 when the finding is first created and MUST increment by one on each material mutation.

**Material mutations** that MUST trigger a version increment:

- `re_scoped` — the finding's boundary or interpretation changed.
- `split` — the finding was decomposed into child findings.
- `merged` — the finding was absorbed into a surviving finding.
- `closed` — the finding's closure criteria were met.
- Closure criteria change — the stated closure criteria were revised after initial statement.

**Routine status transitions** that MUST NOT trigger a version increment:

- `open` → `in_remediation`
- `in_remediation` → `pending_evaluation`
- `pending_evaluation` → `open` (remediation judged insufficient, continuing in current cycle)
- `open` → `carried_forward` (finding passes to a new cycle without material change)

When a packet references a finding record and the reference is sensitive to the finding's state at a specific point in time — such as closure determinations, lineage records, or re-scope justifications — the reference SHOULD include the finding version identifier.

The most recent version of a finding record supersedes all prior versions. Prior versions MUST remain available in version-control history for traceability.

---

## 10. Granularity Requirements

### 10.1 Work Unit Granularity

The local work unit granularity MUST be declared at the start of each cycle.

A work unit is appropriate when ALL of the following hold:

- The unit has one dominant objective.
- The unit maps to one coherent contract-bearing surface.
- Remediation is explainable as one intelligible story.
- Evaluation is able to make a truthful closure determination without hand-waving.
- The unit is small enough to reason about locally but large enough to avoid artificial fragmentation.

Work unit granularity SHOULD become finer as uncertainty narrows:

- Earlier cycles MAY use coarser units when the primary task is clarifying intent or stabilizing the contract.
- Later cycles SHOULD use finer units for targeted remediation, closure, and regression prevention.

In brownfield contexts, work unit granularity SHOULD be finer than in comparable greenfield contexts, because coupling, legacy behavior, and integration risk are harder to predict.

The following failure modes MUST be avoided:

- Units too large to support truthful closure claims.
- Units so small that coherence is lost and context must constantly be re-stitched.

### 10.2 Review Scope Declaration

Every review MUST declare exactly one of the following modes:

**Broad review:**

- Assesses the candidate holistically against the governing contract.
- REQUIRED for major milestones, the first review of a new project, the first review after a governing document revision, architectural changes, or when confidence in local boundaries is low.

**Delta review:**

- Assesses only the changed area plus predictable impact surfaces.
- Appropriate for targeted remediation cycles where issue identity is stable and scope discipline is important.

Review scope MAY widen during a review only when at least one of the following holds:

- A finding cannot be understood without inspecting adjacent abstractions.
- The changed area has obvious downstream callers or dependents.
- Evidence suggests the stated issue is only a local manifestation of a broader defect.
- Documentation drift appears to invalidate the claimed contract.

When scope widens, the reviewer MUST state:

- Why widening was necessary.
- What new boundary was included.
- Whether the widened scope created new findings or recontextualized existing ones.

Out-of-scope work discovered during review MUST be flagged and removed. If scope cannot be determined well enough to identify what is out of scope, scope was not defined sufficiently for work to have started. The work and all downstream work MUST be paused and re-scoped before build resumes.

### 10.3 Handoff Granularity

Handoff granularity MAY legitimately be coarser than local execution granularity.

Coarser handoff packaging is RECOMMENDED when:

- Teams have significant timezone separation.
- Review turnaround is expensive.
- Ownership boundaries require more context to evaluate integration correctly.
- Fragmented delivery would obscure the larger architectural or behavioral thread.
- The receiver is expected to act without relying on local conversational continuity.

A rolled-up handoff MUST still preserve:

- Lineage to underlying work units.
- Finding identity.
- Truthful closure and non-closure claims.
- Evidence links to relevant diffs, packets, and governing documents.

---

## 11. Convergence Loop Requirements

### 11.1 Loop Structure

The convergence loop consists of Phases 4–8: Review → Remediation → Evaluation → Cycle Planning → Handoff (when required).

The loop MUST repeat until one of the termination conditions in Section 11.2 is satisfied.

No phase in the convergence loop MAY be skipped, though fast-track depth MAY be used per Section 8.2.

Phases within the loop MUST be executed in declared sequence:

- Remediation MUST NOT begin before a review packet is produced.
- Evaluation MUST NOT begin before a remediation packet is produced.
- Cycle Planning MUST NOT begin before an evaluation packet is produced.
- Handoff MUST NOT begin before a planning packet with `prepare_handoff` routing is produced.

### 11.2 Termination Conditions

The convergence loop MAY terminate only when one of the following is true:

- All in-scope findings are closed.
- Remaining findings are validly transformed into `split` or `merged` states with preserved lineage and successor routing.
- Remaining items were explicitly re-scoped into a new cycle with preserved identity and rationale.
- The governing documents were judged insufficient and the next required action is document revision rather than further remediation.
- Remaining open findings are explicitly recorded, low severity (`minor` or `informational`), non-blocking relative to the current cycle goal, and their deferral has been explicitly accepted by the human owner.

The loop MUST NOT terminate based on elapsed time, number of passes, or tool state.

### 11.3 Document Revision Trigger Conditions

The process SHOULD prefer document revision over forcing another remediation pass when at least one of the following holds:

- Multiple cycles produce materially similar findings.
- Remediation quality is adequate but review pressure keeps exposing the same ambiguity.
- Evaluators cannot determine success because the acceptance basis is unstated or conflicted.
- The implementation repeatedly exposes a missing architectural or behavioral contract.
- Reviewers and remediators make reasonable but materially incompatible interpretations.

When document revision is triggered:

- The revision MUST become tracked work.
- Prior finding IDs MUST remain linked to the document ambiguity that forced the revision.
- The next cycle MUST explicitly state whether it is validating revised documents, revised implementation, or both.

---

## 12. Closure Requirements

### 12.1 Finding-Level Closure Criteria

A finding MAY be closed only when ALL of the following hold:

- The root issue is addressed.
- No material downstream issue introduced by the remediation remains in the affected area.
- Documentation and comments are aligned with the corrected behavior.
- Test coverage is sufficient for the changed behavior and its predictable regressions.
- The implementation is correct and complete relative to the governing specification.
- The affected area is unlikely to generate immediate, avoidable churn in the next cycle.

A finding MUST NOT be considered resolved merely because a code change occurred.

Tests are supporting evidence of resolution. They are NOT proof of resolution by themselves.

### 12.2 Cycle-Level Closure Criteria

A cycle MAY stop only when one of the termination conditions in Section 11.2 is satisfied.

Cycle-level closure MUST be earned. It MUST NOT be claimed based on visible effort, tool state, or sprint completion.

### 12.3 Low-Severity Deferral Rules

Low-severity (`minor` or `informational`) follow-on findings MAY remain open in the current cycle only if ALL of the following hold:

- They are explicitly recorded as finding records.
- They are non-blocking relative to the current cycle goal.
- Their deferral is explicitly accepted by the human owner.
- Deferral does not falsify any closure claim for the items being closed in the current cycle.

### 12.4 Transformed Finding Terminal States

`split` and `merged` are valid terminal transformed states for a cycle when:

- Successor lineage is explicit.
- Active successor findings are tracked in the next cycle or surviving finding set.
- No closure claim is made for the transformed parent finding itself.

A `split` or `merged` parent finding MUST NOT be treated as closed.

---

## 13. Human and Agent Responsibility Requirements

### 13.1 Human-Controlled Responsibilities

The following responsibilities MUST NOT be delegated to agents:

- Approving governing intent when tradeoffs have meaningful strategic consequences.
- Accepting explicitly documented low-severity (`minor` or `informational`) residual risk.
- Deciding when a document revision materially changes project direction.
- Adjudicating unresolved conflicts between process goals.
- Resolving conflicts between agent outputs (see Section 13.3).
- Making go/no-go decisions at spike decision points.

### 13.2 Agent-Delegable Responsibilities

Agents MAY be delegated the following responsibilities:

- Drafting and revising foundation documents and specifications.
- Implementing against an explicit specification.
- Performing structured reviews.
- Producing review, remediation, evaluation, planning, and handoff packets.
- Tracing lineage, evidence, and closure status when the governing rules are clear.
- Maintaining coherent git references that support packet traceability.
- Selecting and revising local work unit granularity and handoff granularity when the governing rules make the choice explainable.
- Flagging out-of-scope work discovered during execution or review.

An agent MUST NOT treat a decision as safely delegated if the agent cannot explain the routing, granularity, handoff, or closure rationale in packet form.

### 13.3 Agent Failure Mode Requirements

**Out-of-scope work:**

When an agent produces work outside the declared scope, the following MUST occur:

- The out-of-scope work MUST be flagged and removed.
- The affected area and all downstream work MUST be paused.
- The area MUST be re-scoped before build resumes.
- This MUST be treated as evidence of insufficient scope definition upstream, not solely as agent error.

**Conflicting agent outputs:**

When two agents produce materially inconsistent outputs — for example, a review and an evaluation that disagree on closure status for the same finding — the conflict MUST be resolved through the following tiered model:

**Tier 1 — Rule-based agent reconciliation:**

When the conflict falls within explicit, deterministic rules defined in the governing documents — such as severity vocabulary (Section 9.2), status transition rules (Section 9.4), or closure criteria (Section 12.1) — agents MAY resolve the conflict by applying those rules. The resolution MUST be documented in the current packet, including:

- The specific rule applied.
- How the rule determines the correct output.
- Why the conflicting output was incorrect under that rule.

Tier 1 reconciliation is appropriate only when the governing rules unambiguously determine the correct answer. If the agent cannot identify a specific rule that resolves the conflict, Tier 1 MUST NOT be attempted.

**Tier 2 — Human escalation:**

When the conflict involves interpretation, judgment, or ambiguity in the governing documents — or when no deterministic rule resolves the disagreement — the following MUST occur:

- The conflict MUST be escalated to a human for adjudication.
- Agents MUST NOT resolve conflicts that require interpretation or judgment.
- The conflict MUST be treated as a signal that the governing documents contain ambiguity sufficient to support incompatible interpretations.
- The foundation or specification MUST be inspected for the interpretation gap that permitted the divergence.

---

## 14. Document Revision Requirements

### 14.1 When Revision Is Triggered

Governing document revision MUST be triggered when:

- Cycle planning routes to `revise_governing_documents`.
- An evaluation packet recommends document revision.
- A spike identifies governing document insufficiency.

Governing document revision SHOULD be considered when the document revision trigger conditions in Section 11.3 are present.

### 14.2 Revision as Tracked Work

When a governing document revision is triggered:

- The revision MUST be created as tracked work with an explicit reason.
- The reason MUST reference the finding IDs, cycle IDs, or spike records that motivated the revision.
- Prior finding IDs that were linked to the document ambiguity MUST be updated to reference the revision.

### 14.3 Post-Revision Cycle Requirements

After a governing document revision, the next cycle MUST explicitly state whether it is:

- Validating revised documents only.
- Validating revised implementation only.
- Validating both.

The starting scope and packet depth for the post-revision cycle MUST be declared explicitly in the planning packet that triggered the revision.

---

## 15. Process Acceptance Criteria

A process execution SHOULD be considered successful when ALL of the following hold:

- The implemented system matches the current specification.
- The specification remains aligned with the clarified intent in the foundation.
- Architectural boundaries remain coherent under review pressure.
- Documentation and comments remain truthful across cycles.
- Test coverage remains aligned with behavior throughout the convergence loop.
- Repeated cycles decrease rather than proliferate across the project lifecycle.
- Issue history remains traceable across cycles — no finding has been silently dropped, renamed, or implicitly closed.
- Routing decisions are explainable from packet evidence.
- Granularity choices are explainable from coherence, evaluability, and coordination constraints.
- Packet depth choices are explainable from risk and business value.
- Handoff packaging preserves receiver comprehension without falsifying the underlying local work structure.
- Spikes are rare and occur early (Phase 2) rather than during build (Phase 3).
- Tool state is never treated as the basis for a closure or routing decision.
- When churn persists, the process correctly identifies whether the problem lies in code, specification, foundation, or issue framing — and routes accordingly.

---

## 16. Process Health Indicators

> This section is non-normative. It provides recommended quantitative indicators that teams MAY use to detect process health or degradation. These are diagnostic signals, not targets — optimizing for an indicator rather than for the underlying process quality it reflects defeats the purpose.

### 16.1 Convergence Indicators

- **Findings per cycle (trending):** The number of new findings discovered per cycle should decrease over the lifecycle of a project or work item. A sustained increase suggests the specification, implementation, or scope is not converging.
- **Cycle count per work item:** The total number of convergence cycles required to close a work item. Excessive cycle counts suggest scope ambiguity, specification gaps, or remediation quality issues.
- **Re-open rate:** The proportion of findings that return to `open` after evaluation judges remediation insufficient. A high re-open rate suggests remediation is not addressing root causes.

### 16.2 Process Discipline Indicators

- **Spike frequency and phase distribution:** Spikes should be rare overall. When they occur, they should cluster in Phase 2 (specification) rather than Phase 3 (build). A pattern of Phase 3 spikes suggests insufficient upstream definition.
- **Fast-track vs. standard cycle ratio:** The proportion of cycles executed at fast-track depth. An unusually high ratio may suggest the team is under-classifying risk. An unusually low ratio may suggest unnecessary overhead for trivial work.
- **Document revision frequency:** How often governing documents are revised. Frequent revision is not inherently bad — it may indicate healthy responsiveness to convergence signals — but sustained high frequency suggests the intent or specification is unstable.

### 16.3 Closure Quality Indicators

- **Finding age (time in open states):** How long findings remain in non-terminal states. Long-lived open findings may indicate scope problems, unclear closure criteria, or prioritization failures.
- **Transformed finding ratio:** The proportion of findings that reach terminal states via `split`, `merged`, or `re_scoped` rather than direct `closed`. A high ratio suggests initial finding framing is frequently inaccurate.
- **Deferred finding accumulation:** The number of deferred low-severity findings accumulating across cycles. Sustained accumulation without periodic cleanup suggests deferred items are being forgotten rather than managed.

---

*This specification is derived from Process Foundation Document v6 and is governed by the intent, invariants, closed decisions, and philosophy preserved therein.*

---

## Appendix A: Worked Example — Finding Lifecycle

> This appendix is non-normative. It illustrates a single finding moving through the full lifecycle across two convergence cycles, demonstrating how findings, packets, versioning, and routing interact in practice.

### Scenario

**Project:** ACME-API — a REST API for inventory management.
**Motivating driver:** Add batch import endpoint per specification v1.
**Cycle:** ACME-CYC-001

During implementation of a batch import endpoint, a review discovers that the error handling does not match the specification's error model.

---

### Phase 4: Review (Cycle ACME-CYC-001)

The reviewer identifies the issue and creates a finding record:

**Finding record (v1):**

| Field | Value |
|---|---|
| `id` | `ACME-IMPORT-001` |
| `title` | Batch import endpoint returns generic 500 on validation failures instead of per-item 422 responses |
| `originating_cycle` | `ACME-CYC-001` |
| `severity` | `major` |
| `governing_source` | Specification v1, §4.3 (Error Model) |
| `affected_area` | `POST /api/inventory/batch-import` error handling path |
| `status` | `open` |
| `closure_criteria` | 1. Validation failures return per-item 422 responses with field-level error details. 2. Partial success returns 207 Multi-Status. 3. Tests cover all-valid, all-invalid, and mixed batches. |
| `version` | `v1` |

**Review packet snippet (standard depth):**

```
cycle_id: ACME-CYC-001
packet_depth: standard
review_mode: broad
scope_statement: Full implementation of POST /api/inventory/batch-import against Specification v1 §4.
finding_records: [ACME-IMPORT-001]
evidence_notes: "Handler catches all exceptions at the top level and returns 500. The per-item validation
  errors are logged but never surfaced to the caller. Specification §4.3 requires per-item 422 responses."
```

---

### Phase 5: Remediation (Cycle ACME-CYC-001)

The remediating agent transitions the finding to `in_remediation` (no version increment — routine workflow transition) and addresses the root cause.

**Sequencing rationale:** Single finding in this cycle — no sequencing decision required.

**Remediation packet snippet:**

```
cycle_id: ACME-CYC-001
packet_depth: standard
target_finding_ids: [ACME-IMPORT-001]
root_cause_analysis: "The handler used a single try/catch around the entire batch loop. Validation errors
  were caught by the same path as unexpected exceptions. Root cause: no distinction between validation
  failures (expected, per-item) and system errors (unexpected, batch-level)."
changes_made: "Separated validation from execution. Validation errors are now collected per-item and
  returned as 422. System errors still return 500. Partial success returns 207 Multi-Status."
tests_or_validation_performed: "Added tests for: all-valid batch (200), all-invalid batch (422 with
  per-item errors), mixed batch (207 Multi-Status), and system error during processing (500)."
self_assessed_readiness: "Ready for evaluation. All closure criteria addressed."
```

The finding transitions to `pending_evaluation` (no version increment).

---

### Phase 6: Evaluation (Cycle ACME-CYC-001)

The evaluator reviews the remediation and finds it partially addresses the issue:

**Evaluation packet snippet:**

```
cycle_id: ACME-CYC-001
packet_depth: standard
evaluated_finding_ids: [ACME-IMPORT-001]
closure_determination: { "ACME-IMPORT-001": "open" }
evidence_for_closure_or_non_closure: "Closure criteria 1 and 2 are satisfied. Criterion 3 is partially
  satisfied — the mixed-batch test asserts status 207 but does not verify that the response body contains
  both successful and failed item results. The test would pass even if the response body were empty."
downstream_issues_identified: []
documentation_alignment_assessment: "API documentation not yet updated to reflect 207 Multi-Status behavior."
test_coverage_assessment: "Insufficient — mixed-batch test needs body assertions. API docs need update."
next_routing_recommendation: continue_remediation
```

The finding returns to `open` (no version increment — routine transition per §9.7).

---

### Phase 5 (second pass): Remediation (Cycle ACME-CYC-001)

The remediating agent addresses the evaluation feedback:

**Remediation packet snippet (second pass):**

```
cycle_id: ACME-CYC-001
packet_depth: standard
target_finding_ids: [ACME-IMPORT-001]
root_cause_analysis: "Test assertion was incomplete — asserted status code but not response body structure.
  API documentation was not included in the original remediation scope."
changes_made: "1. Added response body assertions to mixed-batch test verifying both success and failure
  items are present. 2. Updated API documentation for POST /api/inventory/batch-import to document
  207 Multi-Status response format."
self_assessed_readiness: "Ready for evaluation. All three closure criteria now fully addressed including
  test body assertions and documentation."
```

---

### Phase 6 (second pass): Evaluation (Cycle ACME-CYC-001)

**Evaluation packet snippet (second pass):**

```
cycle_id: ACME-CYC-001
packet_depth: standard
evaluated_finding_ids: [ACME-IMPORT-001]
closure_determination: { "ACME-IMPORT-001": "closed" }
evidence_for_closure_or_non_closure: "All three closure criteria satisfied: (1) validation failures
  return per-item 422, (2) partial success returns 207 Multi-Status, (3) tests cover all-valid,
  all-invalid, and mixed batches with response body assertions. API documentation updated."
documentation_alignment_assessment: "Aligned."
test_coverage_assessment: "Sufficient."
next_routing_recommendation: close
```

The finding transitions to `closed` — **version increments to v2** (material mutation per §9.7).

---

### Phase 7: Cycle Planning (Cycle ACME-CYC-001)

**Planning packet snippet:**

```
cycle_id: ACME-CYC-001
packet_depth: standard
routing_decision: close
routing_rationale: "All in-scope findings are closed. ACME-IMPORT-001 was the sole finding and is
  now closed with all closure criteria satisfied."
closed_findings: [ACME-IMPORT-001]
governing_document_changes_required: []
```

The cycle closes. No handoff is required (work remains in the same team context).

---

### Key Observations

This example illustrates several process behaviors:

1. **Closure is earned, not declared.** The first evaluation rejected closure because test coverage was insufficient — even though the code change was correct.
2. **Finding version incremented once** — at closure (v1 → v2). The routine workflow transitions (open → in_remediation → pending_evaluation → open → in_remediation → pending_evaluation → closed) did not trigger version increments.
3. **The convergence loop repeated** (review → remediation → evaluation → remediation → evaluation → planning) until the evaluator was satisfied.
4. **Closure criteria were stated before remediation began** (§9.5) and evaluation was judged against those criteria — not against the absence of objections.
5. **Documentation alignment** was assessed as part of evaluation — the first evaluation caught the missing API docs update.
