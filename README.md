# Patterns for Skills

## 1. Foundations
- concepts
- patterns
- rules

## 2. Capabilities
- narrowly scoped but thorough feature coverage
    - defined across:
      1. Domain
      2. Action
      3. Artifact
      4. Constraints
      5. Environment
    - JSON schema, OpenAPI, Zod, Pydantic, PBF, TypeSpec, CUE, etc.

- composable and testable
  - Define what the skill may do and must not do (allowed and disallowed).
  - stable contract, isolated side effects, consistent interface
  - output = skill(input, context)
  - typed inputs and outputs
  - explicit context dependencies
  - declared side effects
  - artifact-oriented composition
    - example: semantic-metric-skill > metric-definition.json > evidence-chart-skill; chart-config.json > evidence-page-skill
  - testing includes:
    - static validation
    - execution validation
    - semantic validation
    - regression validation

- mostly deterministic
  - Structured outputs
  - Intermediate Representations
  - Planner > Typed Skill Graph > Artifact Pipeline > Validators > Repair Loop > Final Output

## 3. Assets
```txt
skills/
  evidence-chart/
    skill.md
    examples/
    anti-patterns.md
    schemas/
    tests/
    retrieval/
    templates/
    evals/
    tool-manifest.json
```

The skill.md defines:
- purpose
- assumptions
- constraints
- style rules
- workflow
- output contract

Examples should be:
- copy/paste runnable
- annotated
- benchmarked

Tests/ should include:
```text
skills/
  evidence-chart/
    tests/
      fixtures/
      snapshots/
      assertions/
      evals/
```

Slash commands should:
- trigger orchestration
- fetch context
- use templates
- execute validation and self-correct

A skill should look like this:
```text
Skill :=
  Intent
  + Capability Boundary
  + Input Schema
  + Context Requirements
  + Execution Policy
  + Output Schema
  + Validation Rules
  + Determinism Constraints
  + Evaluation Harness
```

Natural language > typed intent extraction > validated IR > deterministic transforms > artifact generation > automated verification
