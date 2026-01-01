# Failure Patterns - Structurer Agent

Dieses Dokument sammelt erkannte Fehlermuster für systematische Verbesserung.

---

## FP-struct-001: Zu oberflächliche Strukturen

**Pattern ID:** FP-struct-001
**Agent:** agent-structurer-v1
**Erkannt am:** 2025-12-29
**Häufigkeit:** Initial

### Symptom
- Strukturen bleiben auf Level 1-2
- Unterelemente fehlen oder sind zu generisch
- User muss mehrfach nachprompten für Details

### Root Cause
- Fehlende explizite Tiefenanforderung im Prompt
- Keine Validierung der Strukturtiefe vor Output

### Trigger
```
expected_depth != enforced
output.max_level < 3
```

### Fix
Agent muss vor Output eine Gliederungstiefe >= Level 3 erzwingen.
Selbst-Check vor Ausgabe einführen.

### Status
- [x] Erkannt
- [x] Analysiert
- [ ] In Improvement Rule überführt
- [ ] Validiert

---

## FP-struct-002: Fehlende Leitfragen

**Pattern ID:** FP-struct-002
**Agent:** agent-structurer-v1
**Erkannt am:** 2025-12-29
**Häufigkeit:** Initial

### Symptom
- Struktur hat Überschriften aber keine klaren Ziele
- Unklar, was jede Sektion beantworten soll

### Root Cause
- Leitfragen-Anforderung nicht prominent genug

### Trigger
```
sections.any(s => !s.has_leading_question)
```

### Fix
Jede Hauptsektion MUSS mit "Leitfrage: ..." beginnen.

### Status
- [x] Erkannt
- [x] Analysiert
- [ ] In Improvement Rule überführt
- [ ] Validiert

---

## Template für neue Patterns

```markdown
## FP-struct-XXX: [Kurzbeschreibung]

**Pattern ID:** FP-struct-XXX
**Agent:** agent-structurer-v1
**Erkannt am:** YYYY-MM-DD
**Häufigkeit:** [Initial|Selten|Häufig|Kritisch]

### Symptom
[Was fällt auf?]

### Root Cause
[Warum passiert das?]

### Trigger
[Wann tritt es auf? Bedingungen]

### Fix
[Wie beheben?]

### Status
- [ ] Erkannt
- [ ] Analysiert
- [ ] In Improvement Rule überführt
- [ ] Validiert
```
