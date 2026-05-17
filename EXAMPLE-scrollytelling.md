```text
/Compose-Story-scrollytelling-executive-mobile-safe
```
* `Compose`: multi-artifact assembly (just one artifact would use Create-)
* `Story`: narrative structure domain
* `scrollytelling`: interaction modality
* `executive`: audience
* `mobile`: layout
* `safe`: mutation risk

Skill Manifest
```yaml
skill:
  name: Compose-Story-scrollytelling
  verb_class: Compose
  domain: narrative_analytics
  modality: scrollytelling
  inputs:
    type: object
    required:
      - topic
      - audience
      - datasets
      - metrics
    properties:
      topic: string
      audience: string
      datasets: array
      metrics: array
      constraints: object
  outputs:
    artifacts:
      - narrative_ir
      - layout_ir
      - interaction_ir
      - mdx_page
      - echarts_configs
      - scroll_triggers
  side_effects: []
  determinism: medium_high
  requires:
    - semantic_metric_catalog
    - chart_component_library
    - storytelling_templates
    - evidence_layout_system
  policies:
    max_sections: 12
    max_charts_per_section: 2
    required_progression: true
    mobile_first: true
```

The skill does not directly output MDX, it produces several, layered intermediate representations.

Narrative
```json
{
  "story_arc": "problem_to_insight_to_action",
  "sections": [
    {
      "id": "context",
      "intent": "establish baseline",
      "narrative_role": "setup"
    },
    {
      "id": "trend_shift",
      "intent": "show divergence in KPI",
      "narrative_role": "inciting_event"
    },
    {
      "id": "root_cause",
      "intent": "decompose drivers",
      "narrative_role": "analysis"
    },
    {
      "id": "implications",
      "intent": "business meaning",
      "narrative_role": "resolution"
    }
  ]
}
```
Layout
```json
{
  "breakpoints": ["mobile", "tablet", "desktop"],
  "section_flow": "vertical_scroll",
  "density": "executive_sparse",
  "components": [
    {
      "type": "kpi_band",
      "sticky": true
    },
    {
      "type": "chart_block",
      "transition": "fade_in_on_scroll"
    }
  ]
}
```
Interaction
```json
{
  "scroll_triggers": [
    {
      "on_enter": "section:trend_shift",
      "actions": ["animate_line_growth", "highlight_anomaly"]
    },
    {
      "on_enter": "section:root_cause",
      "actions": ["reveal_stack_breakdown"]
    }
  ]
}
```
Then, after those IRs are created, the execution steps are pleasantly deterministic.

Step 1: MDX
* narrative > mdx_sections
* layout > svelte_components
* interaction > scroll bindings

Step 2: Charts
A dedicated skill like `Generate-EChartsConfig-executive-accessible` is called for each chart, and those are added to the right sections.

Then injected into sections.

The skills are composable into a Pipeline:

```text
Compose-Story-scrollytelling
   ↓
Generate-NarrativeIR
   ↓
Generate-LayoutIR
   ↓
Generate-InteractionIR
   ↓
Generate-EChartsConfigs
   ↓
Validate-ScrollytellingExperience
   ↓
Render-MDXPage
```
Each step is:
* independently testable
* replaceable
* mockable
* evaluable

Then, always validate, with something like `Validate-Story-scrollytelling` that must check:
Structure:
* required narrative arc exists
* section ordering valid
* no orphan sections

UX:
* mobile scroll depth acceptable
* chart density limits respected

Performance:
* number of scroll triggers
* chart render budget
* query cost bounds

Semantics:
* KPI consistency across sections
* no contradictory claims

Example output:
```json
{
  "valid": false,
  "issues": [
    {
      "type": "ux_violation",
      "message": "Too many charts in mobile viewport in section root_cause"
    },
    {
      "type": "semantic_inconsistency",
      "message": "Revenue trend and KPI summary mismatch in section 2"
    }
  ]
}
```

Good skills have:
1. Narrow scope
* narrative analytics experiences
* not general dashboarding
2. Composability
* chart skills
* query skills
* layout skills
3. Testability
* IRs
* deterministic templates
* validation reports
4. Determinism
* IR separation
* constrained rendering
* schema enforcement
* fixed templates

The skill is not a generator, it is a compiler:
- The Narrative IR is like an AST
- The Layout IR is like IR lowering
- The Interaction IR is like the event graph
- The MDX render is like codegen
- The ECharts configs is like a target backend
- The Validation skill is like the type checker

So, `Compose-Story-scrollytelling-executive-mobile-safe` is essentially a domain-specific compiler for narrative analytics UX, with - 
- Outputs:
  * narrative_ir.json
  * layout_ir.json
  * interaction_ir.json
  * charts/*.json
  * page.mdx
  * validation_report.json
- inputs:
  * semantic metrics
  * datasets
  * design system
  * chart library
- Validated by:
  * Validate-Story-scrollytelling

Model the skill as a constrained multi-stage compilation pipeline from semantic intent → interactive narrative runtime

Modeling this way helps verbs, qualifiers, schemas, tests, and composability work intuitively. 
