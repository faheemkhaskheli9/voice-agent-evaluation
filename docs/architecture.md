# Architecture Notes: Voice Agent Batch Testing Platform

## Pipeline

```text
Persona Script -> Simulated Caller -> Voice Agent Under Test -> Recording + Transcript -> Automated Scoring -> Report
```

## Components

- Configurable test personas
- Automated simulated conversations
- Audio recording and archiving
- Automatic transcription
- Response quality evaluation
- Latency measurement per turn
- Conversation-level scoring
- Failed-test detection and flagging

## Design Notes

- Keep provider/model choices swappable behind interfaces (see `multi-llm-router`
  and similar projects in this portfolio for the general pattern).
- Prefer configuration-driven pipelines (YAML/JSON in `configs/`) over hardcoded
  parameters so experiments are reproducible.
