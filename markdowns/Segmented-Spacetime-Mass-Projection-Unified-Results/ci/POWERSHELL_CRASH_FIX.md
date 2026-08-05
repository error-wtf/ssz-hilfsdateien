# PowerShell Extension Crash - Problem & Lösung

## Problem

Wenn Python-Skripte (insbesondere `ci/autorun_suite.py`) direkt in einem PowerShell-Terminal ausgeführt werden, während die **PowerShell Extension** in VS Code/Windsurf aktiv ist, kann es zu **Abstürzen** kommen.

### Ursache

1. Python-Fehlermeldungen enthalten Code-Fragmente wie:
   ```python
   main()
   subprocess.run(command, check=True)
   raise CalledProcessError(retcode, process.args)
   ```

2. Die PowerShell Extension versucht, diese Fragmente zu **parsen**

3. Parse-Fehler führen zu Runtime-Exceptions in PowerShell Editor Services

4. Die Extension stürzt ab und muss neu gestartet werden

### Symptome

- PowerShell Terminal friert ein
- Fehlermeldung: `The PowerShell Extension Terminal has stopped`
- Log-Einträge in `PowerShell.log`:
  ```
  System.Management.Automation.ParseException: At line:1 char:10
  +     main()
  +          ~
  An expression was expected after '('.
  ```
- Automatischer Neustart der Extension

## Lösung

### Option 1: Safe Wrapper (PowerShell)

Verwenden Sie `run_safe.ps1` zum isolierten Ausführen von Python-Skripten:

```powershell
.\ci\run_safe.ps1 -ScriptPath "ci\autorun_suite.py" -Arguments "--config", "ci\suite_config.yaml"
```

**Vorteile:**
- ✅ Python-Output wird umgeleitet
- ✅ Keine Parse-Konflikte mit PowerShell Extension
- ✅ Detaillierte Fehlerprotokolle in separaten Dateien

### Option 2: Batch Wrapper (CMD)

Verwenden Sie `run_suite_safe.bat` für maximale Kompatibilität:

```cmd
.\ci\run_suite_safe.bat
```

oder mit benutzerdefinierter Konfiguration:

```cmd
.\ci\run_suite_safe.bat ci\custom_config.yaml
```

**Vorteile:**
- ✅ Läuft in CMD statt PowerShell (kein Extension-Konflikt)
- ✅ Filtert problematische Output-Zeilen
- ✅ UTF-8 Encoding automatisch gesetzt

### Option 3: Separates Terminal

Öffnen Sie ein **normales CMD/CMD.exe Terminal** (nicht PowerShell):

```cmd
cd H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00
python ci\autorun_suite.py --config ci\suite_config.yaml
```

### Option 4: WSL/Linux

Unter WSL2 oder Linux gibt es dieses Problem nicht:

```bash
cd /mnt/h/WINDSURF/Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00
python ci/autorun_suite.py --config ci/suite_config.yaml
```

## Präventive Maßnahmen

### 1. Log-Rotation einrichten

Verhindert, dass `PowerShell.log` zu groß wird:

```powershell
# Alte Logs archivieren
Rename-Item -Path "PowerShell.log" -NewName "PowerShell.log.old" -ErrorAction SilentlyContinue
```

### 2. Separate Terminals für Python

- **PowerShell Terminal**: Nur für PowerShell-Befehle
- **CMD Terminal**: Für Python-Skripte
- **Git Bash/WSL**: Für Linux-Tools

### 3. VS Code Settings anpassen

Deaktivieren Sie IntelliSense für Python-Output in PowerShell:

```json
{
    "powershell.integratedConsole.showOnStartup": false,
    "powershell.integratedConsole.focusConsoleOnExecute": false
}
```

## Technische Details

### PowerShell Extension Architektur

```
VS Code Extension
    ↓
PowerShell Editor Services (PSES)
    ↓
PowerShell Language Server
    ↓
Parse Output → CRASH wenn Python-Code erkannt wird
```

### Warum passiert das?

Die PowerShell Extension verwendet einen **Language Server**, der versucht, **allen Terminal-Output** zu analysieren, um:
- IntelliSense bereitzustellen
- Syntaxfehler zu erkennen
- Code-Vervollständigung anzubieten

Wenn Python-Code im Output erscheint, versucht der Parser, ihn als PowerShell zu interpretieren → **Parse Exception** → **Crash**

## Weitere Ressourcen

- [PowerShell Extension Issues](https://github.com/PowerShell/vscode-powershell/issues)
- [Python in PowerShell Best Practices](https://docs.microsoft.com/powershell/scripting/dev-cross-plat/vscode/using-vscode)

## Kontakt

Bei weiteren Problemen, erstellen Sie ein Issue im Repository.
