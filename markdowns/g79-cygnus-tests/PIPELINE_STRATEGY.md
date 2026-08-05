# Pipeline-Strategie: Tests DANN Animationen

## ⚠️ Kritisches Design-Prinzip

**Animationen werden NACH allen Tests generiert, nicht währenddessen!**

---

## 🚫 Problem (alte Methode)

Wenn Animationen während der Tests generiert werden:

```
Test 1 → [GIF generieren] → ❌ BLOCKIERT!
   ↓ (matplotlib öffnet Fenster)
   ↓ (Pipeline wartet)
   ↓ (User muss Fenster schließen)
Test 2 → ...
```

**Folgen:**
- Pipeline stoppt und wartet auf User-Interaktion
- Tests laufen nicht automatisch durch
- Lange Wartezeiten (5-10 Minuten pro Animation)
- Nicht geeignet für CI/CD oder automatisierte Runs

---

## ✅ Lösung (neue Methode)

Tests und Animationen sind **getrennt**:

```
PHASE 1: ALLE TESTS (schnell, nicht-blockierend)
  Test 1 ✅ (10s)
  Test 2 ✅ (15s)
  Test 3 ✅ (20s)
  Test 4 ✅ (12s)
  Test 5 ✅ (18s)
  → Gesamt: ~2 Minuten

PHASE 2: ANIMATIONEN (am Ende, im Hintergrund)
  Animation 1 ✅ (30s)
  Animation 2 ✅ (35s)
  Animation 3 ✅ (40s)
  Animation 4 ✅ (30s)
  Animation 5 ✅ (35s)
  → Gesamt: ~3 Minuten

PHASE 3: VARIANTEN (automatisch)
  5s Versionen ✅ (1 min)
  30s Versionen ✅ (1 min)
  → Gesamt: ~2 Minuten

TOTAL: ~7 Minuten (vollautomatisch!)
```

**Vorteile:**
- ✅ Keine User-Interaktion nötig
- ✅ Pipeline läuft durch ohne Stopp
- ✅ Geeignet für automatisierte Systeme
- ✅ Tests schlagen nicht fehl wegen Matplotlib-Problemen
- ✅ Klare Trennung: Tests = Wissenschaft, GIFs = Visualisierung

---

## 🔧 Technische Implementierung

### 1. Nicht-interaktives Matplotlib Backend

**In allen Scripts:**
```python
import matplotlib
matplotlib.use('Agg')  # BEFORE importing pyplot!
import matplotlib.pyplot as plt
```

**Umgebungsvariable:**
```python
os.environ['MPLBACKEND'] = 'Agg'
```

### 2. Tests: Keine Animationen während Ausführung

**RUN_PIPELINE_OPTIMIZED.py:**
```python
# Run tests with non-interactive backend
env = os.environ.copy()
env['MPLBACKEND'] = 'Agg'

subprocess.run(
    [sys.executable, test_script],
    env=env,  # Force non-interactive
    timeout=120
)
```

### 3. Animationen: Separate Phase

**Erst NACH allen Tests:**
```python
if all_tests_passed >= threshold:
    # Now generate animations
    subprocess.run([sys.executable, "GENERATE_TEST_ANIMATIONS.py"])
    subprocess.run([sys.executable, "CREATE_ANIMATION_VARIANTS.py"])
```

---

## 📋 Verwendung

### Für Entwicklung (interaktiv)
```bash
# Tests ansehen (mit detaillierter Ausgabe)
python RUN_ALL_TESTS_COMPLETE.py

# Dann manuell Animationen erstellen
python GENERATE_TEST_ANIMATIONS.py
```

### Für Automatisierung (CI/CD)
```bash
# Alles in einem Durchlauf
python RUN_PIPELINE_OPTIMIZED.py
```

### Für Präsentationen (nur GIFs)
```bash
# Wenn Tests schon gelaufen sind
python GENERATE_TEST_ANIMATIONS.py
python CREATE_ANIMATION_VARIANTS.py
```

---

## 📊 Pipeline-Diagramm

```
┌─────────────────────────────────────────┐
│  START: RUN_PIPELINE_OPTIMIZED.py      │
└────────────────┬────────────────────────┘
                 │
    ┌────────────▼─────────────┐
    │  STAGE 1: PHYSICS TESTS  │
    │  ├─ test_1.py            │
    │  ├─ test_2.py            │
    │  ├─ test_3.py            │
    │  ├─ test_4.py            │
    │  └─ test_5.py            │
    │  (MPLBACKEND=Agg)        │
    │  No plots shown!         │
    └────────────┬─────────────┘
                 │
    ┌────────────▼─────────────────────┐
    │  Check: ≥3 tests passed?         │
    │  YES → Continue                  │
    │  NO  → Skip animations           │
    └────────────┬─────────────────────┘
                 │ YES
    ┌────────────▼───────────────────────┐
    │  STAGE 2: BASE ANIMATIONS          │
    │  GENERATE_TEST_ANIMATIONS.py       │
    │  ├─ gamma_seg_evolution.gif        │
    │  ├─ velocity_excess.gif            │
    │  ├─ energy_release.gif             │
    │  ├─ core_mass_scaling.gif          │
    │  └─ radio_redshift.gif             │
    │  (Background, no windows)          │
    └────────────┬───────────────────────┘
                 │
    ┌────────────▼─────────────────────┐
    │  STAGE 3: VARIANTS               │
    │  CREATE_ANIMATION_VARIANTS.py    │
    │  For each base GIF:              │
    │  ├─ *_5s.gif                     │
    │  ├─ *_30s_repeat.gif             │
    │  └─ *_30s_slow.gif               │
    └────────────┬─────────────────────┘
                 │
    ┌────────────▼─────────────────────┐
    │  STAGE 4: SUMMARY REPORT         │
    │  ├─ Test results                 │
    │  ├─ Animation files              │
    │  ├─ Total time                   │
    │  └─ Success rate                 │
    └────────────┬─────────────────────┘
                 │
            [END: EXIT CODE]
```

---

## 🎯 Zusammenfassung

| Aspekt | Alte Methode | Neue Methode |
|--------|-------------|-------------|
| **Blockierung** | Ja (matplotlib Fenster) | Nein (Agg backend) |
| **User-Interaktion** | Erforderlich | Nicht nötig |
| **Automatisierung** | Unmöglich | Vollständig |
| **Durchlaufzeit** | >30 Minuten (mit Warten) | ~7 Minuten |
| **CI/CD tauglich** | ❌ Nein | ✅ Ja |
| **Tests unabhängig** | ❌ Nein (gekoppelt) | ✅ Ja (getrennt) |

---

## 💡 Best Practices

1. **Tests schreiben:** Keine `plt.show()` aufrufen!
   ```python
   # ❌ FALSCH
   plt.plot(x, y)
   plt.show()  # BLOCKIERT!
   
   # ✅ RICHTIG
   plt.plot(x, y)
   plt.savefig('output.png')
   plt.close()
   ```

2. **Backend setzen:** Immer vor pyplot import
   ```python
   import matplotlib
   matplotlib.use('Agg')  # FIRST!
   import matplotlib.pyplot as plt
   ```

3. **Animationen:** Separate Scripts für GIF-Generierung
   - Nicht in Test-Scripts einbauen
   - Nur in dedizierten Animation-Scripts

4. **Pipeline:** Optimierten Runner verwenden
   - `RUN_PIPELINE_OPTIMIZED.py` für Automatisierung
   - Nicht Test-Scripts direkt mit Animation-Code mischen

---

© 2025 Carmen N. Wrede, Lino P. Casu, Bingsi  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
