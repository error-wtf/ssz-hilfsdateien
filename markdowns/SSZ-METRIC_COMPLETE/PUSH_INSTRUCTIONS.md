# Push Instructions for ssz-metric-pure

**Status:** ✅ Alle Änderungen lokal committed (17 commits)  
**Problem:** ⚠️ Kein Remote-Repository konfiguriert  
**Lösung:** Remote hinzufügen und pushen

---

## Option 1: Zu GitHub Pushen (Empfohlen)

### Schritt 1: GitHub Repository erstellen

1. Gehe zu https://github.com/new
2. Repository Name: `ssz-metric-pure`
3. Description: "Pure Segmented Spacetime (SSZ) metric - singularity-free black holes"
4. Visibility: **Public** oder **Private**
5. ⚠️ **WICHTIG:** Keine README, .gitignore oder LICENSE hinzufügen (wir haben die schon!)
6. Click "Create repository"

### Schritt 2: Remote hinzufügen & pushen

```bash
cd E:\clone\ssz-metric-pure

# Remote hinzufügen (ersetze USERNAME mit deinem GitHub Username)
git remote add origin https://github.com/USERNAME/ssz-metric-pure.git

# Oder mit SSH (wenn SSH-Key konfiguriert):
git remote add origin git@github.com:USERNAME/ssz-metric-pure.git

# Branch umbenennen zu main (GitHub Standard)
git branch -M main

# Pushen
git push -u origin main
```

### Schritt 3: Verifizieren

```bash
git remote -v
# Sollte zeigen:
# origin  https://github.com/USERNAME/ssz-metric-pure.git (fetch)
# origin  https://github.com/USERNAME/ssz-metric-pure.git (push)
```

---

## Option 2: Zu GitLab Pushen

### Schritt 1: GitLab Projekt erstellen

1. Gehe zu https://gitlab.com/projects/new
2. Project name: `ssz-metric-pure`
3. Visibility: **Public** oder **Private**
4. ⚠️ **Initialize repository with README** NICHT ankreuzen!
5. Click "Create project"

### Schritt 2: Remote hinzufügen & pushen

```bash
cd E:\clone\ssz-metric-pure

# Remote hinzufügen
git remote add origin https://gitlab.com/USERNAME/ssz-metric-pure.git

# Oder mit SSH:
git remote add origin git@gitlab.com:USERNAME/ssz-metric-pure.git

# Pushen
git push -u origin master
```

---

## Option 3: Zu eigenem Server Pushen

```bash
cd E:\clone\ssz-metric-pure

# Remote hinzufügen (ersetze SERVER und PATH)
git remote add origin ssh://USER@SERVER/PATH/ssz-metric-pure.git

# Pushen
git push -u origin master
```

---

## Nach dem Push: Repository Archivieren

### GitHub:

1. Gehe zu Repository → Settings
2. Scroll nach unten zu "Danger Zone"
3. Click "Archive this repository"
4. Bestätige mit Repository-Namen
5. ✅ Repository ist jetzt read-only

### Topics hinzufügen (Optional):

```
black-holes
general-relativity
segmented-spacetime
golden-ratio
singularity-free
pure-ssz
metric-tensor
```

### README Badge updaten:

Ändere in README.md:
```markdown
[![Status](https://img.shields.io/badge/status-alpha-orange)]()
```

Zu:
```markdown
[![Status](https://img.shields.io/badge/status-archived-red)]()
[![Archive](https://img.shields.io/badge/archive-incomplete-yellow)]()
```

---

## Troubleshooting

### Fehler: "Authentication failed"

**Lösung:** Verwende Personal Access Token statt Passwort

1. GitHub → Settings → Developer settings → Personal access tokens
2. Generate new token (classic)
3. Scope: `repo` (full control)
4. Kopiere Token
5. Bei Push: Username = dein GitHub Username, Password = Token

### Fehler: "Remote already exists"

**Lösung:** Alten Remote entfernen

```bash
git remote remove origin
# Dann erneut hinzufügen (siehe oben)
```

### Fehler: "Permission denied (publickey)"

**Lösung:** SSH-Key hinzufügen oder HTTPS verwenden

```bash
# HTTPS statt SSH verwenden:
git remote set-url origin https://github.com/USERNAME/ssz-metric-pure.git
```

---

## Schnell-Kommando (Copy-Paste Ready)

**Für GitHub (HTTPS):**
```bash
cd E:\clone\ssz-metric-pure
git remote add origin https://github.com/USERNAME/ssz-metric-pure.git
git branch -M main
git push -u origin main
```

**Für GitLab (HTTPS):**
```bash
cd E:\clone\ssz-metric-pure
git remote add origin https://gitlab.com/USERNAME/ssz-metric-pure.git
git push -u origin master
```

---

## Nach dem Push

✅ Repository ist online  
✅ 17 Commits gepusht  
✅ Alle Dokumentation verfügbar  
✅ Bereit für Archive  

**Jetzt:**
1. Repository archivieren (siehe oben)
2. Eventuell README Badge updaten
3. Topics/Tags hinzufügen
4. Fertig! 🎉

---

© 2025 Carmen N. Wrede & Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
