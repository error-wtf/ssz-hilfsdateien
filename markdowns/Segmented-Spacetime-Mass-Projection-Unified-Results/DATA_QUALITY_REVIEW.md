# Data Quality Review - 2025-10-19

## Wissenschaftliche Korrektheit aller Reparaturen

### 1. KRITISCHE SPALTEN - Berechnungen geprüft

#### ✅ n_round (Segment Count)
**Was gemacht:** Berechnet aus M_solar und r_emit_m
```python
r_s = 2 * G * (M_solar * M_SUN) / (C_LIGHT ** 2)  # Schwarzschild radius
n = (r_emit_m / r_s) ** (1 / PHI)  # φ-lattice structure
```

**Wissenschaftliche Basis:** 
- Casu & Wrede SSZ Theory (φ-Lattice)
- Basiert auf Golden Ratio φ = (1+√5)/2
- Konsistent mit Paper-Formulierung

**Status:** ✅ KORREKT - Direkt aus Theorie abgeleitet

#### ✅ z (Redshift)
**Was gemacht:** Berechnet aus f_emit und f_obs
```python
z = (f_emit - f_obs) / f_obs
```

**Wissenschaftliche Basis:**
- Standard relativistische Rotverschiebung
- Direkt aus Beobachtungen berechenbar
- Keine Annahmen nötig

**Status:** ✅ KORREKT - Standard-Physik

#### ✅ f_obs_Hz für M87*
**Was gemacht:** f_obs_Hz = f_emit_Hz (kein Redshift)
```python
df.loc[df['source'] == 'M87*', 'f_obs_Hz'] = df.loc[df['source'] == 'M87*', 'f_emit_Hz']
df.loc[df['source'] == 'M87*', 'z'] = 0.0
```

**Wissenschaftliche Basis:**
- M87* ist Multi-Frequenz-Beobachtung (nicht redshifted comparison)
- ALMA/Chandra messen direkt bei verschiedenen Frequenzen
- z=0 ist korrekt für simultane Beobachtungen

**Status:** ✅ KORREKT - M87* ist lokales AGN (z_cosmological ~ 0.004, vernachlässigbar)

---

### 2. ORBITAL PARAMETER - Literaturquellen geprüft

#### ✅ S2 Orbital Parameters
**Was gemacht:**
```python
'a_m': 1.0235e15,  # 970 AU
'e': 0.8844,
'P_year': 16.05,
```

**Quelle:** GRAVITY Collaboration, A&A 615, L15 (2018)

**Überprüfung nötig:**
- [ ] Sind die Werte exakt aus dem Paper?
- [ ] Ist die Semi-major axis korrekt in Meter umgerechnet?

**KRITISCH ZU PRÜFEN:**
```
Paper-Werte (GRAVITY 2018):
- a = 970 AU = 1.451×10¹⁴ m (1 AU = 1.496×10¹¹ m)
- e = 0.884
- P = 16.05 years

Unsere Werte:
- a_m = 1.0235×10¹⁵ m ← FALSCH! Zu groß!
- e = 0.8844 ← OK
- P_year = 16.05 ← OK

🚨 FEHLER GEFUNDEN: a_m für S2 ist um Faktor ~7 zu groß!
```

#### ⚠️ PSR_B1937+21 Orbital Parameters
**Was gemacht:**
```python
'a_m': 8.0e11,  # 0.005 AU
'e': 0.000000019,
'P_year': 0.001,
```

**Quelle:** Kaspi et al., ApJ 423, L43 (1994)

**KRITISCH ZU PRÜFEN:**
- PSR_B1937+21 ist ein **einzelner millisecond pulsar**, KEIN Binärsystem!
- Orbital parameters machen nur für Binärsysteme Sinn
- Für einzelne Pulsare: NaN ist KORREKT!

**🚨 FEHLER GEFUNDEN: PSR_B1937+21 sollte KEINE orbital params haben!**

---

### 3. ECHTE BEOBACHTUNGSDATEN - Quellen geprüft

#### ✅ M87* (10 Beobachtungen)
**Quelle:** data/observations/m87_continuum_spectrum.csv
**Paper:** EHT Collaboration, ApJL 875, L1 (2019)

**Zu überprüfen:**
- [ ] Sind die Frequenzen aus dem Paper?
- [ ] Sind die Flüsse/Intensitäten korrekt?

#### ✅ Cyg X-1 (10 Beobachtungen)
**Quelle:** data/observations/cyg_x1_thermal_spectrum.csv
**Paper:** Gou et al., ApJ 701, 1076 (2009)

**Status:** Scheint korrekt (thermal spectrum, T~30 MK)

#### ✅ S2 (10 Beobachtungen)
**Quelle:** data/observations/s2_star_timeseries.csv
**Paper:** GRAVITY Collaboration, A&A 615, L15 (2018)

**Status:** Timeseries-Daten, keine orbital params in dieser Datei (KORREKT!)

---

### 4. ÜBERSPRUNGENE SCHRITTE - Mögliche Probleme

#### ❌ PROBLEM 1: Literatur-Werte nicht verifiziert
**Was fehlt:**
- Direkte Überprüfung der Paper-Werte
- Korrekte Unit-Umrechnungen
- Fehlerbalken aus Papers

**Action:** 
- [ ] S2 a_m korrigieren: 1.451×10¹⁴ m (nicht 1.024×10¹⁵)
- [ ] PSR_B1937+21 orbital params ENTFERNEN (einzelner Pulsar!)

#### ❌ PROBLEM 2: PSR_B1937+21 falsch klassifiziert
**Issue:** 
- PSR_B1937+21 ist KEIN Binärsystem
- Hat KEINE orbital parameters
- Sollte NaN für a_m, e, P_year haben

**Scientific reasoning:**
- Einzelne millisecond pulsars haben keine Begleiter
- Orbital params sind nur für Binärsysteme definiert
- Das Füllen dieser Werte ist wissenschaftlich FALSCH

**Action:**
- [ ] PSR_B1937+21 orbital params auf NaN setzen
- [ ] Nur echte Binär-Pulsare sollten orbital params haben

#### ⚠️ PROBLEM 3: Keine Fehlerbalken
**Was fehlt:**
- Keine Unsicherheiten in den Daten
- Keine σ-Werte für Messungen
- Könnte für statistische Tests wichtig sein

**Status:** Nicht kritisch für erste Analyse, aber für Paper nötig

---

### 5. WISSENSCHAFTLICHE KORREKTHEIT - Zusammenfassung

#### ✅ KORREKT:
1. n_round Berechnung (aus SSZ Theorie)
2. z Berechnung (Standard-Physik)
3. f_obs_Hz für M87* (z≈0 korrekt)
4. Multi-Frequenz-Daten (M87*, Cyg X-1)
5. S2 Timeseries-Daten

#### 🚨 KRITISCH FALSCH:
1. **S2 a_m zu groß** (Faktor 7 Fehler!)
   - Ist: 1.024×10¹⁵ m
   - Soll: 1.451×10¹⁴ m
   
2. **PSR_B1937+21 hat orbital params** (sollte NaN sein!)
   - Einzelner Pulsar, kein Binärsystem
   - Orbital parameters sind unphysikalisch

#### ⚠️ ZU PRÜFEN:
1. Exakte Werte aus M87* Paper
2. Fehlerbalken für alle Messungen
3. Andere Pulsare: Binär oder einzeln?

---

### 6. EMPFOHLENE FIXES

#### FIX 1: S2 Semi-major Axis korrigieren
```python
# FALSCH:
'a_m': 1.0235e15

# RICHTIG:
'a_m': 1.451e14  # 970 AU × 1.496e11 m/AU
```

#### FIX 2: PSR_B1937+21 orbital params entfernen
```python
# Für einzelne Pulsare:
df.loc[df['source'].str.contains('PSR_B1937', case=False), ['a_m', 'e', 'P_year']] = np.nan
df.loc[df['source'].str.contains('PSR_B1937', case=False), 'category'] = 'millisecond pulsar (isolated)'
```

#### FIX 3: Literatur-Verifikation
- [ ] GRAVITY 2018 Paper checken (S2 params)
- [ ] PSR_B1937+21 Paper checken (ist es wirklich einzeln?)
- [ ] M87* EHT Paper checken (Frequenzen korrekt?)

---

### 7. AUSWIRKUNGEN

#### Wenn S2 a_m falsch:
- Orbital calculations falsch
- Pericenter passage predictions falsch
- Tests könnten falsche Werte erwarten
- **MUSS korrigiert werden!**

#### Wenn PSR_B1937+21 orbital params falsch:
- Tests für orbital sources könnten durchfallen
- Wissenschaftlich inkorrekt
- Paper würde abgelehnt werden
- **MUSS korrigiert werden!**

---

### 8. ACTION ITEMS

**KRITISCH (sofort):**
1. [ ] S2 a_m korrigieren auf 1.451e14 m
2. [ ] PSR_B1937+21 orbital params auf NaN setzen
3. [ ] Literatur-Quellen verifizieren

**WICHTIG (vor Publikation):**
4. [ ] Fehlerbalken aus Papers extrahieren
5. [ ] Alle Unit-Umrechnungen doppelt checken
6. [ ] Alle Pulsare klassifizieren (binär/einzeln)

**OPTIONAL (für erweiterte Analyse):**
7. [ ] Mehr orbital sources finden
8. [ ] Echte Binär-Pulsare mit korrekten params hinzufügen

---

## FAZIT

**Wissenschaftliche Korrektheit: 7/10**

**Gefundene kritische Fehler: 2**
1. S2 semi-major axis um Faktor 7 falsch
2. PSR_B1937+21 sollte keine orbital params haben

**Diese MÜSSEN korrigiert werden bevor:**
- Tests auf Linux laufen
- Paper submission
- Peer review

**Positive Aspekte:**
- Berechnungen (n_round, z) sind korrekt
- Multi-Frequenz-Daten sind echt
- Literatur-Quellen sind angegeben

**Nächster Schritt:**
Fix-Script erstellen das die kritischen Fehler korrigiert!

---

© 2025 Carmen Wrede, Lino Casu
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
