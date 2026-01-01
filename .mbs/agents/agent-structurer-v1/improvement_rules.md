# Improvement Rules - Structurer Agent

Automatisch angewandte Regeln zur Agentenverbesserung.

---

## IR-struct-001: Tiefenerzwingung

**Regel ID:** IR-struct-001
**Abgeleitet von:** FP-struct-001
**Aktiv seit:** 2025-12-29

### Bedingung
```
IF prompt_type == "structuring"
AND iterations_count >= 3
AND output_quality IN ["poor", "ok"]
```

### Aktion
- Erhöhe automatisch die geforderte Struktur-Tiefe auf Level 4
- Füge explizite Beispielstruktur in den Prompt ein
- Aktiviere Selbst-Validierung vor Output

### Prompt-Ergänzung
```
WICHTIG: Prüfe vor Ausgabe:
- Hat jede Hauptsektion mindestens 2 Unterebenen?
- Ist die maximale Tiefe >= 3?
Falls nein: Erweitere die Struktur.
```

---

## IR-struct-002: Leitfragen-Pflicht

**Regel ID:** IR-struct-002
**Abgeleitet von:** FP-struct-002
**Aktiv seit:** 2025-12-29

### Bedingung
```
IF output.sections.any(s => !s.leading_question)
```

### Aktion
- Nachträgliche Aufforderung zur Leitfragen-Ergänzung
- Template mit Beispiel-Leitfragen bereitstellen

### Prompt-Ergänzung
```
Jede Hauptsektion beginnt mit:
> Leitfrage: [Was soll diese Sektion klären?]
```

---

## IR-struct-003: Iterationsbasierte Eskalation

**Regel ID:** IR-struct-003
**Abgeleitet von:** Allgemein
**Aktiv seit:** 2025-12-29

### Bedingung
```
IF prompt_type == "structuring"
AND iterations_count > 5
```

### Aktion
- Wechsel zu detaillierterem Prompt-Template
- Verlange explizit Beispiele oder Diagramm-Hinweise
- Aktiviere Debugging-Modus mit Begründungen

### Prompt-Ergänzung
```
Da mehrere Iterationen nötig waren:
1. Erkläre deine Strukturentscheidungen
2. Gib für jeden Hauptzweig ein konkretes Beispiel
3. Markiere unsichere Bereiche mit [?]
```

---

## Template für neue Regeln

```markdown
## IR-struct-XXX: [Regelname]

**Regel ID:** IR-struct-XXX
**Abgeleitet von:** [FP-ID oder "Allgemein"]
**Aktiv seit:** YYYY-MM-DD

### Bedingung
[Wann wird die Regel angewandt?]

### Aktion
[Was passiert?]

### Prompt-Ergänzung
[Welcher Text wird eingefügt?]
```
