Names are important.

Slash command names can communicate:
- semantic contract
- routing
- capability
- UX affordance
- orchestration hints
- determinism constraints

They can encode:
- intent
- side effects
- expected output
- operational categories
- composability

Naming pattern: <verb>-<noun>[-modifier]
- Verb → operational intent
- Artifact → primary domain objec
- Qualifier(s) → scope, modality, environment, constraints, or workflow specialization

| (Inspired by: PowerShell cmdlets, REST, RPC, compiler, CI/CD actions, Unix commands, k8s verbs, git verbs)

Verbs specify actions, side effects, determinism expectations and pipeline position.

Nouns specify Artifacts and artifact types.

Modifiers specify Scope. They narrow ambiguity, constrain execution, hint at determinism, improve discoverability, and stabilize orchestration. They're additive, orthogonal, and machine-parsable. They can define domain, output, environment, constraint, workflow-stage, determinism, audience

Verbs have a few categories to make them useful and consistent.
- Read/Inspect verbs have no side effects.
  - for example, Get, Inspect, Analyze, Explain, etc.
- Validation verbs are for assertions
  - for example, Test, Verify, Lint
- Creation verbs make stuff
  - for example, Generate, Make, etc.
- Mutation
- Execution
- etc.

Commands have encoded capability classes too.
- Analyze-* - Read-only
- Validate-* - Assertions only
- Generate-* - New artifacts
- Refactor-* - Controlled mutation
- Publish-* - External side effects

Command specifies intent, but the contract/schema drives implementation details.

Examples:
```text
Generate-EvidenceChart
Compose-ExecutiveDashboard
Validate-DuckDBQuery
Optimize-EvidenceBuild
Refactor-MetricDefinitions
Publish-AnalyticsSite
Audit-KPIGovernance
Explain-QueryPlan
Trace-DataLineage
```

Command names allow both users and orchestrators to infer:
* side effects
* scope
* outputs
* confidence expectations
* execution class
* rollback implications

## Read
Read verbs are safe and idempotent:
```text
Get
List
Inspect
Describe
Explain
Trace
Compare
Analyze
Profile
```
Think:
* HTTP GET
* PowerShell Get
* Unix inspection

## Validation
Validation verbs check and assert
```text
Validate
Verify
Test
Lint
Audit
Check
```
Think:
* CI systems
* compiler passes
* policy engines

## Creation
Creation verbs make stuff.
```text
Generate
Compose
Scaffold
Derive
Synthesize
Transform
```
Think:
* compiler emit

## Mutation
Mutation verbs change stuff.
```text
Update
Refactor
Optimize
Normalize
Reconcile
Migrate
Patch
Apply
```
Think:
* HTTP PATCH/PUT
* k8s apply

## Execution
Execution verba run stuff.
```text
Run
Invoke
Execute
Publish
Deploy
Export
Import
Sync
```
Think:
* RPC
* deployment pipelines

## Governance
Governance verbs control stuff.
```text
Authorize
Approve
Review
Attest
Sign
Enforce
```
