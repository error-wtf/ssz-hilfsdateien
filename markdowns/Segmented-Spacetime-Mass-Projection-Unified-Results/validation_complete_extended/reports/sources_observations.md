# Beobachtungsquellen-Inventar (lokale Dateien)

ASCII-Vorschau:
```
+---------------------+-----------------------------------------------------------------------------------------------+
| Objekt              | Dateien (lokal)                                                                               |
+---------------------+-----------------------------------------------------------------------------------------------+
| G79.29+0.46         | Ammonia_observations_in_the_LBV_nebula_G7929046_Di.pdf; Jiménez-Esteban_2010_ApJ_713_429 (1).pdf; |
|                     | stu296.pdf; 0804.0266v1.pdf                                                                   |
+---------------------+-----------------------------------------------------------------------------------------------+
| CygnusX_DiamondRing | The_Diamond_Ring_in_Cygnus_X_Advanced_stage_of_an_.pdf; The_AKARI_diffuse_maps.pdf            |
+---------------------+-----------------------------------------------------------------------------------------------+
```

**JSON (roh, maschinenlesbar):**
```json
{
  "G79.29+0.46": {
    "papers_local": [
      "Ammonia_observations_in_the_LBV_nebula_G7929046_Di.pdf",
      "Jiménez-Esteban_2010_ApJ_713_429 (1).pdf",
      "stu296.pdf",
      "0804.0266v1.pdf"
    ],
    "tracers": {
      "HII": ["cm free-free"],
      "PDR": ["[C II] 158um", "[O I]", "PAH"],
      "Molecular": ["CO(1-0)", "CO(2-1)", "CO(3-2)", "NH3(1,1)", "NH3(2,2)"]
    },
    "notes": "Innerer CO-Clump mit low-velocity shock ~14–15 km/s; kalte NH3/CO-Clumps nahe der Front."
  },
  "CygnusX_DiamondRing": {
    "papers_local": [
      "The_Diamond_Ring_in_Cygnus_X_Advanced_stage_of_an_.pdf",
      "The_AKARI_diffuse_maps.pdf"
    ],
    "tracers": {
      "PDR": ["[C II] 158um"],
      "Molecular": ["CO(1-0)"]
    },
    "notes": "Ringförmige [C II]-Emission; vrad = 1.3 ± 0.6 km/s."
  }
}
```
