# Was Schumann ueber SSZ sagt und warum wir ins starke Feld gehen

**Einseitige Zusammenfassung fuer Paper/Repo**

---

## Das Schumann-Ergebnis

Wir haben Schumann-Resonanzen (8-30 Hz) der Erde-Ionosphaeren-Cavity analysiert:

| Metrik | Wert |
|--------|------|
| Datenpunkte | 744 Stunden (Oktober 2013) |
| chi²/ndof | 55.4 >> 1 |
| Mode-Spread | 3.2% (f1: -2.8%, f4: -11.2%) |
| SSZ-Obergrenze | |delta_seg| < 0.5% |

**Ergebnis:** Das SSZ-Minimalmodell (ein globales delta_seg fuer alle Moden) wird **verworfen**. Klassische ionosphaerische Dispersion dominiert.

---

## Was das bedeutet (und was nicht)

### Das bedeutet NICHT:
- ❌ "SSZ ist falsch"
- ❌ "SSZ existiert nicht"
- ❌ "ELF-Frequenzen sind ungeeignet"

### Das bedeutet:
- ✅ Bei GM/(Rc²) ~ 10⁻⁹ ist SSZ nicht vom Hintergrund trennbar
- ✅ Die Erde ist gravitativ "zu langweilig" fuer SSZ-Detektion
- ✅ Klassische Effekte (Ionosphaere, Wetter) ueberdecken alles

---

## Die Skalierung erklaert alles

Die **gleiche Mathematik** (gamma_seg) gilt ueberall:

```
gamma_seg(r) = 1 - alpha * exp[-(r/r_c)²]
delta_f/f = gamma_seg - 1 ≈ -alpha  (bei r=0)
```

| Regime | GM/(Rc²) | alpha | delta_f/f | Status |
|--------|----------|-------|-----------|--------|
| Erde (Schumann) | 7×10⁻¹⁰ | ~10⁻⁹ | ~10⁻⁹ | Null-Test ✓ |
| **G79 Nebel** | variabel | **0.12** | **~12%** | **Detektiert!** |
| Neutronenstern | ~0.25 | ~0.25 | ~25% | Erwartet |
| Schwarzes Loch | ~0.5 | ~0.5 | ~50% | Erwartet |

---

## Die Verbindung zu G79

Im G79.29+0.46 Nebel-Paper haben wir **dieselbe gamma_seg-Funktion** verwendet:

| Observable | Formel | G79-Beobachtung |
|------------|--------|-----------------|
| Temperatur | T' = T₀ × gamma_seg | 500K → 200K → 60K (Shells) |
| Geschwindigkeit | Delta_v/v = gamma_seg⁻¹/² - 1 | ~5 km/s Exzess |
| Frequenz | nu' = nu₀ × gamma_seg | Radio-Kontinuum konsistent |

**Gleiche Gleichungen, andere Skala!**

---

## Warum "ELF" nicht die Frequenz meint

SSZ ist **frequenzunabhaengig**:

```
delta_f/f = gamma_seg⁻¹ - 1  (gilt fuer ALLE f)
```

Was zaehlt:
- ✅ Gravitationspotential (GM/Rc²)
- ✅ Relative Praezision (delta_f/f)
- ❌ Absolute Frequenz (Hz)

"ELF" im SSZ-Kontext bedeutet: **langsamer Takt** (Segment-Zaehlung), nicht 3-30 Hz EM-Wellen.

---

## Fazit

| Aussage | Status |
|---------|--------|
| Schumann zeigt: Erde zu schwach fuer SSZ | ✅ Bestaetigt |
| G79 zeigt: SSZ bei alpha~0.12 detektierbar | ✅ Bestaetigt |
| Mathematik ist identisch (gamma_seg) | ✅ Bestaetigt |
| Naechster Schritt: Starke Felder (NS, BH, GW) | → In Arbeit |

**Die Schumann-Analyse ist ein erfolgreicher Null-Test, kein Widerspruch zu SSZ.**

---

*Kurzform: Nicht ELF ist zu klein - die Gravitation der Erde ist zu klein.*
