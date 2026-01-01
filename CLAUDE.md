# CLAUDE.md - Agentic Master Workspace (AMW) Learning System

## Überblick

Dieses Repository implementiert das **AMW Learning System** - ein Framework für Prompt-Tracking, Zeitmessung und Agenten-Selbstverbesserung.

## Ordnerstruktur

```
.mbs/                              # Master Brain Storage (Hidden)
├── config.json                    # Systemkonfiguration
├── schema.json                    # JSON-Schema für Datenmodelle
├── events.json                    # Event-Log (E13-E17)
├── prompts/<work_id>/             # Prompt-Records pro Work
│   └── p-XXXX.json
├── logs/<work_id>/                # Session-Logs & Timing
│   ├── session.log
│   └── timing.json
└── agents/                        # Agenten-Definitionen
    ├── registry.json
    └── <agent_id>/
        ├── agent.json             # Definition, Guardrails, Metriken
        ├── prompt_template.md     # Lernfähiges Template
        ├── failure_patterns.md    # Erkannte Fehlermuster
        └── improvement_rules.md   # Automatische Verbesserungsregeln
```

## Agenten-Typen

| Agent | Rolle | Hauptaufgabe |
|-------|-------|--------------|
| `agent-sense-maker-v1` | Sense-Maker | Intent & Work-Type Erkennung |
| `agent-structurer-v1` | Structurer | Logische Strukturen & Gliederungen |
| `agent-producer-v1` | Producer | Content-Erstellung nach Vorgabe |
| `agent-refiner-v1` | Refiner | Qualitätsverbesserung |
| `agent-archivist-v1` | Archivist | Wissensarchivierung & Indexierung |

## Prompt-Tracking

Jede Prompt-Interaktion wird als Record gespeichert:

```json
{
  "prompt_id": "p-0001",
  "work_id": "w-20251229-xxx",
  "agent_id": "agent-structurer-v1",
  "prompt_type": "structuring",
  "output_quality": "poor|ok|good|excellent",
  "human_feedback": "...",
  "followup_required": true
}
```

**Regel:** Wenn `followup_required: true` ≥ 3× für gleichen `prompt_type` → Failure Pattern extrahieren.

## Lernpipeline

1. **Prompt ausführen** → Record speichern
2. **Nachprompten erkannt** → Implizites Feedback
3. **Pattern-Erkennung** → Iterationen + Qualität analysieren
4. **Failure Pattern extrahieren** → `failure_patterns.md` erweitern
5. **Improvement Rule ableiten** → `improvement_rules.md` erweitern
6. **Template anpassen** → `prompt_template.md` verbessern

## Event-Typen

| Event | Beschreibung |
|-------|--------------|
| `E13` | PROMPT_EXECUTED |
| `E14` | PROMPT_FEEDBACK_IMPLICIT |
| `E15` | AGENT_RULE_UPDATED |
| `E16` | FAILURE_PATTERN_DETECTED |
| `E17` | IMPROVEMENT_APPLIED |

## Arbeitsanweisungen

### Neuen Work starten
1. Work-ID generieren: `w-YYYYMMDD-<hash>`
2. Ordner anlegen: `.mbs/prompts/<work_id>/` und `.mbs/logs/<work_id>/`
3. Sense-Maker für Intent-Erkennung nutzen

### Prompt dokumentieren
- Nach jeder Agent-Aktion `p-XXXX.json` erstellen
- `output_quality` ehrlich bewerten
- Bei Nachprompt: `followup_required: true`

### Failure Pattern erkennen
Wenn:
- Gleicher `prompt_type` ≥ 3×
- `output_quality` in `["poor", "ok"]`
- Ähnliches Feedback

→ Pattern in `failure_patterns.md` dokumentieren

### Agent verbessern
1. Pattern analysieren (Root Cause)
2. Improvement Rule formulieren
3. Prompt Template anpassen
4. Guardrails in `agent.json` ergänzen

## Done Criteria (v1.1)

- [ ] Jede Prompt-Interaktion ist nachvollziehbar
- [ ] Zeit & Iterationen sind messbar
- [ ] Failure Patterns sind explizit
- [ ] Agentenbeschreibungen sind versionierbar & lernfähig
- [ ] Verbesserungen passieren automatisch, nicht ad hoc
