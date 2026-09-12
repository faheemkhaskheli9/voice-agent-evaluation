# Persona schema

A persona is a YAML file describing how a simulated caller behaves during a
voice-agent test. It is loaded into the `vae.persona.Persona` pydantic model
before use; unknown keys are rejected.

Annotated template: [`configs/persona_template.yaml`](../configs/persona_template.yaml).
Examples: [`examples/personas/`](../examples/personas/).

## Fields

| Field | Type | Required | Default | Notes |
|-------|------|----------|---------|-------|
| `name` | string | yes | — | Short unique label. Non-empty. |
| `goal` | string | yes | — | One-sentence caller objective. |
| `tone` | string | yes | — | Caller demeanour, e.g. `calm`, `frustrated`, `hurried`. |
| `sample_utterances` | list of string | yes | — | ≥ 1 item, each non-empty. Ordered things the caller might say. |
| `success_criteria` | list of string | yes | — | ≥ 1 item, each non-empty. Conditions marking the call a pass. |
| `max_turns` | int | no | `12` | Hard cap on caller turns. Range `1..100`. |
| `language` | string | no | `"en"` | ISO code, length `2..10`. |
| `metadata` | map of string→string | no | `{}` | Free-form tags (suite, ticket id, severity, …). |

## Validation

```bash
python -m vae.cli validate examples/personas/frustrated_billing.yaml
python -m vae.cli validate examples/personas/            # whole directory
python -m vae.cli show examples/personas/curious_new_customer.yaml
```

Errors are reported per field, e.g.:

```
error: invalid persona broken.yaml:
  - success_criteria: List should have at least 1 item after validation, not 0
  - tone: Field required
```
