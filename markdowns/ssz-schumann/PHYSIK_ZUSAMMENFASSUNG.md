# SSZ Schumann-Analyse: Physik-Zusammenfassung

**Fuer:** Carmen  
**Von:** Lino (via Cascade)  
**Datum:** 2025-12-08

---

## Was wir gemacht haben

Wir haben 744 Stunden echte Schumann-Resonanz-Daten (Oktober 2013, Sierra Nevada) genommen und gefragt:

> "Kann ein einziger, globaler SSZ-Faktor alle vier Schumann-Moden gleichzeitig erklaeren?"

## Was wir gefunden haben

**Nein.**

Die Moden verhalten sich so:

| Mode | Abweichung vom Kugelmodell |
|------|---------------------------|
| f1 (7.8 Hz) | -2.8% |
| f2 (14 Hz) | -8.7% |
| f3 (20 Hz) | -9.6% |
| f4 (26 Hz) | -11.2% |

Das ist **nicht** was SSZ vorhersagt. SSZ sagt: "Alle Moden verschieben sich um den gleichen Prozentsatz."

Stattdessen sehen wir: Je hoeher die Mode, desto groesser die Abweichung. Das ist klassische **ionosphaerische Dispersion** - die Ionosphaere ist kein perfekter Spiegel, und hoehere Frequenzen "sehen" ihre Unvollkommenheiten staerker.

## Was das bedeutet (und was nicht)

### FALSIFIZIERT

> "SSZ ist der Hauptgrund fuer die Schumann-Abweichungen"

Das stimmt nicht. Die Ionosphaere macht den Loewenanteil.

### NICHT FALSIFIZIERT

> "SSZ existiert ueberhaupt nicht"

Das koennen wir mit Schumann nicht sagen. Falls SSZ existiert, ist es:
- Kleiner als ~1%
- Versteckt unter der viel groesseren klassischen Dispersion
- Mit diesem Experiment nicht auflösbar

## Warum das eigentlich gut ist

1. **Wir haben ehrlich getestet.** Keine Schoenfaerberei.
2. **Wir haben ein klares Ergebnis.** chi²/ndof = 55 ist eindeutig.
3. **Wir wissen jetzt, wo wir NICHT suchen muessen.**

Schumann-Resonanzen sind fuer SSZ-Tests ungeeignet - zu viel klassische Physik im Weg.

## Wo wir stattdessen suchen sollten

| Observable | Warum besser? |
|------------|---------------|
| **Atomuhren** | Klassische Physik gut verstanden, 10^-18 Praezision |
| **Gravitationswellen** | GW170817 hat schon |c_gw - c|/c < 10^-15 gemessen! |
| **Kavitaetsresonatoren** | Kontrollierte Umgebung, keine Ionosphaere |

## Die Kurzversion

> "Wir haben's ehrlich getestet. Die Erde schreit: 'Ionosphaere first, SSZ wenn ueberhaupt als leises Fluestern im Hintergrund.'" 🌍📡

Das ist kein Misserfolg - das ist Wissenschaft. Wir haben eine Hypothese aufgestellt, sie getestet, und sie wurde (in dieser Form) widerlegt. Jetzt wissen wir mehr als vorher.

---

## Technische Details (falls jemand fragt)

- **Daten:** 744 Stunden, Sierra Nevada ELF Station, Oktober 2013
- **Methode:** Lorentzian-Fit an FFT-Spektren, Chi-squared-Test
- **Code:** `ssz_analysis/core.py`, `scripts/run_ssz_analysis_v2.py`
- **Reproduzierbar:** `python scripts/run_ssz_analysis_v2.py --use-synthetic-proxies`

---

*"Negative Ergebnisse sind auch Ergebnisse."* - Jeder Wissenschaftler ever
