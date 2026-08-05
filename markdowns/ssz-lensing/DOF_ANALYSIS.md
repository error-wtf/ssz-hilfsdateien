# Degrees of Freedom Analysis - No-Fit Lens Inversion

## Das Problem: Constraints vs Parameter

Ein Quad-Lens liefert **4 Bildpositionen** = **8 skalare Constraints** (x,y pro Bild).

Die Frage ist: **Wie viele Parameter kann man damit eindeutig bestimmen?**

---

## DOF-Tabelle: Aktuelle Parametrisierung

| Modell | Parameter | Anzahl | Constraints | Status |
|--------|-----------|--------|-------------|--------|
| **m=2 (Basis)** | β_x, β_y, θ_E, a_2, b_2, φ_2 | 6 | 8 | ✅ Überbestimmt (+2) |
| **m=2 + Shear** | + γ, φ_γ | 8 | 8 | ⚠️ Genau bestimmt |
| **m=2 + m=3** | + a_3, b_3, φ_3 | 9 | 8 | ❌ Unterbestimmt (-1) |
| **m=2 + m=3 + m=4** | + a_4, b_4, φ_4 | 12 | 8 | ❌ Unterbestimmt (-4) |
| **+ Power-Law η** | + η | +1 | 8 | ❌ Verschärft Problem |
| **+ Linsenzentrum** | + x_L, y_L | +2 | 8 | ❌ Verschärft Problem |

---

## Warum Grid-Search "Pseudo-Fitting" ist

Aktuelle Parametrisierung verwendet **(Amplitude, Phase)**:
- Quadrupol: (a_2, b_2, φ_2) → φ_2 ist **nichtlinear**
- Shear: (γ, φ_γ) → φ_γ ist **nichtlinear**
- Oktupol: (a_3, b_3, φ_3) → φ_3 ist **nichtlinear**

Das erzwingt **Grid-Search über Phasen** → das ist effektiv ein Fit!

---

## Lösung: Reine Komponentenform (Sin/Cos-Basis)

Statt (A, φ) verwende (c, s) mit:
```
A·cos(m·θ - φ) = c·cos(m·θ) + s·sin(m·θ)
```

wobei c = A·cos(φ), s = A·sin(φ).

### Neue Parametrisierung (vollständig linear!)

| Term | Alt | Neu | Linear? |
|------|-----|-----|---------|
| Quadrupol | a_2, b_2, φ_2 | a_2, b_2 | ✅ Ja |
| Shear | γ, φ_γ | γ_1, γ_2 | ✅ Ja |
| Oktupol | a_3, b_3, φ_3 | a_3, b_3 | ✅ Ja |
| Hexadekapol | a_4, b_4, φ_4 | a_4, b_4 | ✅ Ja |

**Wichtig:** Die (a_m, b_m) im aktuellen Code sind bereits die Sin/Cos-Komponenten!
Das Problem ist nur φ_2, φ_3, φ_4 als separate Phase.

---

## Korrigierte DOF-Tabelle (Komponentenform)

| Modell | Parameter | Anzahl | Constraints | Status |
|--------|-----------|--------|-------------|--------|
| **m=2** | β_x, β_y, θ_E, a_2, b_2 | 5 | 8 | ✅ +3 Redundanz |
| **m=2 + Shear** | + γ_1, γ_2 | 7 | 8 | ✅ +1 Redundanz |
| **m=2 + m=3** | + a_3, b_3 | 7 | 8 | ✅ +1 Redundanz |
| **m=2 + Shear + m=3** | alle | 9 | 8 | ❌ -1 (unterbestimmt) |
| **m=2 + m=3 + m=4** | + a_4, b_4 | 9 | 8 | ❌ -1 (unterbestimmt) |

---

## Zusatzdaten für unterbestimmte Fälle

| Zusätzliche Observable | Neue Constraints | Ermöglicht |
|------------------------|------------------|------------|
| **Flux Ratios** (4 Bilder) | +3 (relativ) | m=2 + Shear + m=3 |
| **Time Delays** (4 Bilder) | +3 (relativ) | m=2 + Shear + m=3 |
| **Extended Arc** (N Punkte) | +2N | Beliebig viele Parameter |
| **Linsengalaxie-Licht** | +2 (Zentrum) | Zentrum fixieren |
| **Stellare Kinematik** | +1 (η oder M) | Radialslope |

---

## Empfehlung: "No-Fit" strikt einhalten

### Für Quad-Lens (8 Constraints):

1. **Maximal 7 Parameter** für überbestimmtes System
2. **Nutze die +1 Redundanz** als Konsistenzcheck (h(params) = 0)
3. **Kombinationen die funktionieren:**
   - m=2 allein (5 Param) → 3 Konsistenz-Checks
   - m=2 + Shear (7 Param) → 1 Konsistenz-Check
   - m=2 + m=3 (7 Param) → 1 Konsistenz-Check

### Was NICHT geht ohne Zusatzdaten:
- m=2 + Shear + m=3 (9 > 8)
- m=2 + m=3 + m=4 (9 > 8)
- Jedes Modell mit freiem Zentrum (+2) UND mehreren Multipolen

---

## Diagnose der aktuellen Ergebnisse

| System | m=2 Residuum | m=3 Residuum | Interpretation |
|--------|--------------|--------------|----------------|
| Q2237+0305 | 0.069" | 0.016" | m=3 hilft, aber 0.016" >> 0.003" |
| HE0435-1223 | 0.067" | 0.029" | m=3 hilft, aber immer noch zu groß |

**Bedeutung:**
- "PASS" = Solver konvergiert, nicht "Modell erklärt Daten"
- Residuen > 0.01" = Modell ist physikalisch unzureichend
- Mögliche Ursachen: fehlendes Shear + Multipol kombiniert, oder η ≠ 2

---

## Implementierungsvorschlag

```python
class LinearMultipoleModel:
    """
    Vollständig lineares Multipol-Modell.
    
    Keine Grid-Search nötig - direkter solve.
    """
    
    def unknowns(self):
        # Alle Parameter sind linear!
        params = ['beta_x', 'beta_y', 'theta_E']
        if self.include_shear:
            params += ['gamma_1', 'gamma_2']  # Nicht (gamma, phi)!
        for m in range(2, self.m_max + 1):
            params += [f'a_{m}', f'b_{m}']    # Keine phi_m!
        return params
    
    def invert(self, images):
        A, b = self.build_linear_system(images)
        n_params = len(self.unknowns())
        n_constraints = len(b)
        
        if n_constraints > n_params:
            # Überbestimmt: löse Teilsystem, prüfe Rest
            p = np.linalg.solve(A[:n_params], b[:n_params])
            residuals = A[n_params:] @ p - b[n_params:]
            consistency = np.max(np.abs(residuals))
            return {'params': p, 'consistency': consistency}
        elif n_constraints == n_params:
            # Genau bestimmt: eindeutige Lösung
            return {'params': np.linalg.solve(A, b)}
        else:
            raise ValueError(f"Unterbestimmt: {n_params} Parameter > {n_constraints} Constraints")
```

---

## Fazit

1. **Die aktuelle φ_m-Parametrisierung erzwingt Grid-Search** → das ist faktisch Fitting
2. **Mit (a_m, b_m) statt (A_m, φ_m) wird alles linear** → echter No-Fit
3. **DOF-Zählung ist hart:** Quad-Lens = max 7-8 Parameter
4. **Residuen >> 0.003" zeigen Modell-Unzulänglichkeit** → legitime Diagnose
5. **Für mehr Parameter braucht man mehr Daten** (Fluxes, Delays, Arcs)
