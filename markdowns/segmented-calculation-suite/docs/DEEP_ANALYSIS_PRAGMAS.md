# Deep Analysis Pragmas

## Überblick

Die `deep_analysis.py` prüft den Code auf deprecated patterns und potenzielle Fehler.
Manchmal sind bestimmte Patterns **intentional** (z.B. GR-Helper-Funktionen).
Diese werden mit **Pragmas** explizit markiert.

## Pragma-Format

```python
# deep_analysis: allow-gr-helper func=<function_name>
def <function_name>(...):
    ...
```

## Beispiel: GR-Helper

```python
# deep_analysis: allow-gr-helper func=z_from_dilation
def z_from_dilation(D: float) -> float:
    """
    GR Helper: Redshift from time dilation factor.
    
    NOTE: This is a standard GR formula (z = 1/D - 1), NOT the SSZ formula.
    SSZ redshift uses z_ssz() which correctly applies z_gr × (1 + Δ(M)/100).
    """
    return 1.0 / D - 1.0
```

## Wie der Checker funktioniert

1. **Allowlist** in `deep_analysis.py`:
   ```python
   GR_HELPER_ALLOWLIST = [
       ("methods/redshift.py", "z_from_dilation", "z = 1/D"),
       ("methods/redshift.py", "z_from_dilation", "1.0 / D - 1.0"),
   ]
   ```

2. **Bulletproof Regex** extrahiert `func=<name>` direkt aus dem Pragma:
   ```python
   match = re.search(r'deep_analysis:\s*allow-gr-helper\s+func=(\w+)', line)
   ```

3. **Strenge Prüfung**: Pattern ist NUR erlaubt wenn:
   - Datei stimmt (`methods/redshift.py`)
   - Funktion ist pragma-markiert (`func=z_from_dilation`)
   - Pattern erscheint innerhalb dieser Funktion

## Neuen GR-Helper hinzufügen

1. Pragma direkt über der Funktion:
   ```python
   # deep_analysis: allow-gr-helper func=my_new_gr_helper
   def my_new_gr_helper(...):
   ```

2. Allowlist in `deep_analysis.py` erweitern:
   ```python
   GR_HELPER_ALLOWLIST = [
       ...
       ("methods/myfile.py", "my_new_gr_helper", "pattern_to_allow"),
   ]
   ```

3. Tests laufen lassen: `python deep_analysis.py`

## Regeln

- **NIE** Pragmas nutzen um echte SSZ-Fehler zu verstecken
- **NUR** für klar abgegrenzte GR-Helper oder Legacy-Code
- **IMMER** im Docstring dokumentieren warum es kein SSZ ist
- Allowlist so **eng wie möglich** halten: (datei, funktion, pattern)

## Aktuelle Allowlist

| Datei | Funktion | Pattern | Grund |
|-------|----------|---------|-------|
| `methods/redshift.py` | `z_from_dilation` | `z = 1/D` | GR-Helper für Standard-GR-Redshift |
| `methods/redshift.py` | `z_from_dilation` | `1.0 / D - 1.0` | GR-Helper Implementation |

## Verhaltenskodex

```
Bei Pattern-Alarm:
1. IDENTIFIZIEREN: Exakte Fundstelle + Repro
2. ENTSCHEIDEN: Bug vs Intentional Design
3. PATCHEN: Pragma + Allowlist (eng begrenzt)
4. TESTEN: Komplette Testkette
5. REPORTEN: Diff-Summary + Commit-Message

Goldene Regel:
False Positive eliminieren OHNE echte Fehler zu übersehen.
Checker strenger machen, nicht weicher!
```
