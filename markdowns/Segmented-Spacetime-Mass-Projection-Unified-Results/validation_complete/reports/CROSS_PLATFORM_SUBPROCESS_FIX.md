# Cross-Platform Subprocess Output Fix

**Datum:** 2025-10-18  
**Status:** ✅ Funktioniert auf Windows + Linux

---

## 🔴 **Das Problem**

### **Symptom:**
```
--- Running lagrangian_tests.py --object sun ---
                                                ← KEIN OUTPUT!
--- Running lagrangian_tests.py --object sgrA ---
                                                ← KEIN OUTPUT!
```

### **Ursache:**
1. **Windows:** Verwendet `cp1252` encoding (nicht UTF-8)
2. **Lösung:** `sys.stdout = io.TextIOWrapper(...)` für UTF-8
3. **ABER:** TextIOWrapper blockiert subprocess-Output!
4. Child-Prozesse können nicht mehr direkt schreiben

---

## ✅ **Die Lösung**

### **Zwei-Stufen-Ansatz:**

#### **Stufe 1: Platform-abhängiges stdout-Setup**

```python
IS_WINDOWS = sys.platform.startswith('win')

if IS_WINDOWS:
    # Windows: TextIOWrapper für UTF-8 (cp1252 → UTF-8)
    try:
        sys.stdout.reconfigure(encoding="utf-8", errors="replace")
    except:
        sys.stdout = io.TextIOWrapper(
            sys.stdout.buffer, 
            encoding="utf-8", 
            errors="replace", 
            line_buffering=True  # ← WICHTIG: Sofortiges Flushen
        )
else:
    # Linux: Meist schon UTF-8, nur sicherstellen
    try:
        sys.stdout.reconfigure(encoding="utf-8", errors="replace")
    except:
        pass  # Schon UTF-8, kein Problem
```

#### **Stufe 2: Explizite stdout/stderr-Bindung**

```python
def run(cmd, cwd=None):
    subprocess.run(
        cmd,
        stdout=sys.stdout,  # ← KRITISCH: Explizit binden!
        stderr=sys.stderr,  # ← KRITISCH: Explizit binden!
        encoding="utf-8",
        errors="replace",
        ...
    )
```

**Warum das funktioniert:**
- `stdout=sys.stdout` sagt subprocess **EXPLIZIT** wo es hinschreiben soll
- Funktioniert mit TextIOWrapper UND normalem stdout
- Cross-platform kompatibel

---

## 🧪 **Testing**

### **Windows:**
```powershell
python run_all_ssz_terminal.py
```

**Erwartet:**
```
--- Running ... lagrangian_tests.py --object sun ---
==============================================================================
LAGRANGIAN TESTS — Sun | M = 1.988470E+30 kg | eps3 = 0
==============================================================================
Schwarzschild radius r_s : 2.952893E+03 m
Photon sphere r_ph       : 4.429340E+03 m
...
```

### **Linux:**
```bash
python3 run_all_ssz_terminal.py
```

**Erwartet:**
```
--- Running ... lagrangian_tests.py --object sun ---
==============================================================================
LAGRANGIAN TESTS — Sun | M = 1.988470E+30 kg | eps3 = 0
==============================================================================
Schwarzschild radius r_s : 2.952893E+03 m
Photon sphere r_ph       : 4.429340E+03 m
...
```

---

## 📝 **Geänderte Datei**

**`run_all_ssz_terminal.py`:**

### **Änderung 1: Platform-Detection (Zeile 23-48)**
```python
IS_WINDOWS = sys.platform.startswith('win')

if IS_WINDOWS:
    # Windows-spezifisches UTF-8 Setup
    ...
else:
    # Linux-spezifisches UTF-8 Setup
    ...
```

### **Änderung 2: subprocess.run() mit stdout-Binding (Zeile 96-126)**
```python
def run(cmd, cwd=None):
    subprocess.run(
        cmd,
        stdout=sys.stdout,  # Explizit
        stderr=sys.stderr,  # Explizit
        ...
    )
```

### **Änderung 3: Fallback-Mechanismus (Zeile 118-126)**
```python
except Exception as e:
    # Fallback ohne stdout-Binding
    subprocess.run(cmd, ...)  # Retry
```

---

## 🎯 **Warum kein separates Skript?**

**Ein Skript für beide Systeme:**
- ✅ Weniger Wartung
- ✅ Keine Duplikate
- ✅ Platform-Detection zur Laufzeit
- ✅ Automatische Anpassung

**Statt:**
```
run_all_ssz_terminal_windows.py  ❌
run_all_ssz_terminal_linux.py    ❌
```

**Haben wir:**
```
run_all_ssz_terminal.py  ✅ (Universal)
```

---

## 🔧 **Technische Details**

### **Windows-Probleme:**

1. **cp1252 Encoding:**
   - Windows Console nutzt Code Page 1252
   - Griechische Buchstaben (β, γ, φ) → Crash
   - **Lösung:** UTF-8 via TextIOWrapper

2. **TextIOWrapper blockiert subprocess:**
   - Wrapped stdout hat andere Referenz
   - subprocess findet echten stdout nicht
   - **Lösung:** Explizites `stdout=sys.stdout`

3. **Line Buffering:**
   - `line_buffering=True` sorgt für sofortigen Output
   - Ohne: Output erst am Ende sichtbar

### **Linux-Unterschiede:**

1. **UTF-8 Standard:**
   - Linux nutzt meist UTF-8 von Haus aus
   - `reconfigure()` reicht meistens

2. **Subprocess-Output:**
   - Normalerweise kein Problem
   - Explizites Binding schadet aber nicht

3. **Environment:**
   - `LC_ALL=C.UTF-8` setzt Locale
   - `PYTHONIOENCODING=utf-8` für Child-Prozesse

---

## ⚠️ **Wichtig für neue Skripte**

**IMMER wenn subprocess.run() verwendet wird:**

```python
# ✅ RICHTIG (Cross-Platform):
subprocess.run(
    cmd,
    stdout=sys.stdout,      # Explizit!
    stderr=sys.stderr,      # Explizit!
    encoding="utf-8",
    errors="replace",
    env=_utf8_env()
)

# ❌ FALSCH (Kann Output verschlucken):
subprocess.run(cmd)  # Ohne stdout/stderr
```

---

## 🚀 **Status**

```
✅ Windows: UTF-8 encoding + subprocess output
✅ Linux: UTF-8 encoding + subprocess output
✅ Fallback-Mechanismus bei Fehlern
✅ Cross-platform kompatibel
✅ Ein Skript für beide Systeme
✅ Keine Duplikate nötig
```

---

## 📊 **Vergleich Vorher/Nachher**

### **Vorher:**
```
Windows:
- ❌ Output verschwindet
- ❌ UnicodeEncodeError bei Griechisch

Linux:
- ✅ Output funktioniert
- ⚠️ Kann bei wrapped stdout auch fehlen
```

### **Nachher:**
```
Windows:
- ✅ Output sichtbar
- ✅ UTF-8 funktioniert
- ✅ Griechische Zeichen OK

Linux:
- ✅ Output sichtbar
- ✅ UTF-8 sichergestellt
- ✅ Kompatibel mit Windows-Code
```

---

## 🔍 **Debugging**

**Wenn Output noch fehlt:**

1. **Prüfe Platform-Detection:**
   ```python
   print(f"Platform: {sys.platform}")
   print(f"IS_WINDOWS: {IS_WINDOWS}")
   ```

2. **Prüfe stdout-Setup:**
   ```python
   print(f"stdout type: {type(sys.stdout)}")
   print(f"stdout encoding: {sys.stdout.encoding}")
   print(f"has buffer: {hasattr(sys.stdout, 'buffer')}")
   ```

3. **Prüfe subprocess-Binding:**
   ```python
   # Füge Debug-Output in run() ein:
   print(f"stdout before run: {sys.stdout}")
   subprocess.run(..., stdout=sys.stdout, ...)
   ```

4. **Test einzelnes Skript direkt:**
   ```bash
   # Windows:
   python lagrangian_tests.py --object sun
   
   # Linux:
   python3 lagrangian_tests.py --object sun
   ```

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
