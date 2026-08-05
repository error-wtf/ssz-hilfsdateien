# Real Data Verification - "NO SYNTHETIC DATA" Claim

## Critical Review: Was ist echt vs. berechnet?

### ✅ ERLAUBT (Theoriebasiert oder trivial ableitbar):

1. **n_round (Segment Count)**
   - Status: BERECHNET aus SSZ-Theorie
   - Formel: `n = (r / r_s)^(1/φ)` (φ-Lattice)
   - Begründung: **Theoriespezifisch**, kann nicht gemessen werden
   - **ERLAUBT** ✓

2. **z (Redshift)**
   - Status: BERECHNET aus f_emit und f_obs
   - Formel: `z = (f_emit - f_obs) / f_obs`
   - Begründung: Triviale Umrechnung aus gemessenen Frequenzen
   - **ERLAUBT** ✓ (wenn f_emit und f_obs echt sind!)

3. **r_s (Schwarzschild radius)**
   - Status: BERECHNET aus M_solar
   - Formel: `r_s = 2GM/c²`
   - Begründung: Physikalische Konstante, direkt aus Masse
   - **ERLAUBT** ✓

---

### ⚠️ KRITISCH ZU PRÜFEN:

#### 1. M87* f_obs_Hz = f_emit_Hz
**Was wir gemacht haben:**
```python
df.loc[df['source'] == 'M87*', 'f_obs_Hz'] = df.loc[df['source'] == 'M87*', 'f_emit_Hz']
df.loc[df['source'] == 'M87*', 'z'] = 0.0
```

**Ist das wissenschaftlich korrekt?**
- M87* hat kosmologisches z ~ 0.0042 (Virgo Cluster)
- Für lokale Analyse: z ≈ 0 ist OK (Fehler < 0.5%)
- **ABER:** f_obs sollte aus Paper kommen, nicht einfach = f_emit!

**Problem:** 
Wir haben die 10 M87* Datenpunkte mit f_obs_Hz gefüllt durch Kopieren von f_emit_Hz.
Das ist **NICHT** echt, das ist eine Annahme!

**Lösung:** 
- [ ] Prüfen ob data/observations/m87_continuum_spectrum.csv f_obs enthält
- [ ] Falls ja: Diese Werte nutzen
- [ ] Falls nein: M87* Rows müssen f_obs aus EHT Paper haben

#### 2. S2 Orbital Parameters
**Was wir gemacht haben:**
- a_m, e, P_year aus GRAVITY 2018 Paper geholt
- **Status:** ✅ ECHT (aus Paper)

**ABER:**
Die 10 S2 Datenpunkte in data/observations/s2_star_timeseries.csv haben:
- Nur: orbital_phase, f_emit_Hz, f_obs_Hz, r_emit_m, v_los_mps
- **NICHT**: a_m, e, P_year

**Was wir dann gemacht haben:**
Wir haben a_m, e, P_year zu allen S2 rows hinzugefügt.

**Ist das OK?**
- **JA** - Diese Parameter sind konstant für S2
- Es sind echte Werte aus GRAVITY 2018
- Wir haben sie nur "propagiert" zu allen Beobachtungen

**Status:** ✅ OK

---

### 🚨 PROBLEMATISCHE DATEN:

#### Problem 1: 127 "alte" Datenpunkte
**Frage:** Woher kommen die ursprünglichen 127 Datenpunkte?

**Zu prüfen:**
- [ ] Sind das echte Beobachtungen aus Papers?
- [ ] Oder waren das "synthetic/placeholder" Daten?
- [ ] Welche Sources sind das genau?

**Action:** Alle 177 rows durchgehen und Source checken

#### Problem 2: M87* f_obs_Hz
**Status:** ⚠️ POTENTIELL FAKE

Wir haben einfach f_obs_Hz = f_emit_Hz gesetzt.
Das ist wissenschaftlich nur OK wenn:
1. z << 1 (stimmt für M87*)
2. Wir nur Frequenz-Vergleich machen (nicht Redshift)
3. Im Paper sind f_obs Werte nicht gegeben

**Wenn im EHT Paper f_obs GEGEBEN ist:**
→ Wir MÜSSEN diese Werte nutzen, nicht f_emit kopieren!

---

### 📋 ACTION ITEMS:

#### KRITISCH (vor Paper):

1. [ ] **M87* f_obs_Hz verifizieren**
   - EHT Paper checken: Gibt es observed frequencies?
   - Falls ja: Diese nutzen (nicht f_emit kopieren!)
   - Falls nein: Dokumentieren warum f_obs = f_emit OK ist

2. [ ] **Alle 177 Quellen verifizieren**
   - Liste aller unique sources erstellen
   - Für jede Source: Paper-Referenz checken
   - Synthetic/placeholder Quellen ENTFERNEN

3. [ ] **Cyg X-1 Daten verifizieren**
   - Sind die 10 thermal spectrum points echt?
   - Paper: Gou et al. 2009 - Daten checken

4. [ ] **S2 Timeseries verifizieren**
   - Sind die 10 observations echt?
   - GRAVITY 2018 - Daten checken

#### WICHTIG (für Peer Review):

5. [ ] Fehlerbalken für alle Messungen
6. [ ] Alle Paper-Referenzen in Sources.md
7. [ ] Data provenance für jede Zeile

---

### 🎯 EMPFEHLUNG:

**Script erstellen das:**
1. Alle 177 rows analysiert
2. Source classification macht (echt vs. berechnet vs. fraglich)
3. Für jede Source: Paper-Referenz checkt
4. Problematische rows identifiziert
5. Report generiert

**Dann:**
- Problematische rows ENTFERNEN oder durch echte Daten ersetzen
- README anpassen falls nötig
- Sources.md vervollständigen

---

### 📊 REALITÄTSCHECK:

**Was wir behaupten (README):**
```
⚠️  NO SYNTHETIC DATA
All 167 data points are from peer-reviewed observations:
- 30 ALMA/Chandra/VLT observations (M87*, Cyg X-1, S2)
- 137 additional real observations
```

**Was wir haben müssen:**
- ✅ 30 ALMA/Chandra/VLT: OK wenn Papers gecheckt
- ⚠️ 137 "additional": **WO KOMMEN DIE HER?**

**Kritische Frage:**
Sind die 137 "additional" Datenpunkte wirklich alle aus Papers?
Oder waren das vorher synthetic/placeholder Daten?

---

## FAZIT:

**Wissenschaftliche Korrektheit aktuell: 7/10**

**Kritische Punkte:**
1. M87* f_obs_Hz = f_emit_Hz (möglicherweise fake)
2. Herkunft der 137 "additional" Datenpunkte unklar
3. Keine Fehlerbalken

**Nächster Schritt:**
Vollständige Quellen-Verifikation aller 177 rows!

---

© 2025 Carmen Wrede, Lino Casu
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
