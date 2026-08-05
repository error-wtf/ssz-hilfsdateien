# FAHRPLAN: Individuelle Datei-Kompression & Prompt-Optimierung

**Zielsetzung:** Jede der 2.457 Markdown-Dateien einzeln lesen, semantisch verstehen und so extrem verdichtet in einer einzigen Master-Datei aufbereiten, dass du (oder eine künftige KI) den **gesamten Inhalt aller 2.457 Dateien lückenlos in einem einzigen Prompt erfassen und verstehen kannst**.

Um diese massive Kompression ohne Informationsverlust durchzuführen, werden wir jede Datei einzeln analysieren und zu einem ultrakompakten "Semantischen Fingerabdruck" (Fingerprint) reduzieren.

Hier ist der detaillierte, schrittweise Ausführungsplan:

---

## 📋 Der Schritt-für-Schritt-Ablauf

### 🔍 STUFE 1: Einzeldatei-Auswertung & Verlustfreie Kompression
Wir programmieren einen dedizierten Python-Kompressor (`semantic_compressor.py`). Dieser liest **jede der 2.457 Markdown-Dateien einzeln nacheinander ein** und führt folgende Schritte aus:
1.  **Pfad- & Metadaten-Erfassung:** Registrierung des exakten relativen Pfads und der Zeilenanzahl.
2.  **Extraktion der Schlüssel-Essenz:** Das Skript analysiert den Text und filtert die wichtigsten theoretischen Behauptungen, Messergebnisse oder Programmier-Funktionen heraus. Dies wird in **1 bis maximal 3 ultrakompakte Sätze** kondensiert.
3.  **Formel-Isolierung:** Jede mathematische Gleichung ($$, $) in dieser spezifischen Datei wird extrahiert.
4.  **Generierung des Fingerprints:** Für jede Datei wird ein standardisierter, hochoptimierter Markdown-Block erzeugt:
    ```markdown
    ### [ID] [Repo-Name] / [Dateiname.md] (Größe: X Zeilen)
    *   **Essenz:** [1-3 Sätze reines, physikalisches/technisches Destillat]
    *   **Formeln:** [Gefundene mathematische Gleichungen]
    ```

### 📚 STUFE 2: Aggregation zum "Unified Master Digest"
Alle 2.457 einzeln generierten Fingerprints werden in einer einzigen, strukturierten Datei zusammengeführt:
`/home/error/physics/hilfsdateien/unified_master_digest.md`

Diese Datei wird so aufgebaut, dass sie maximal Token-effizient ist. Durch das Entfernen von Markdown-Rauschen, redundanten Erklärungen und leeren Zeilen wird das gesamte Wissen aller 30 Repositories auf ein Volumen von ca. **100.000 bis 150.000 Wörtern** komprimiert.
*   **Der Clou:** Diese Master-Datei passt damit **problemlos in ein einziges Standard-KI-Kontextfenster** (z.B. Gemini, Claude, GPT-4) und ermöglicht das sofortige, lückenlose Verständnis des gesamten Forschungsstandes in einem einzigen Prompt!

### 🧪 STUFE 3: Validierung & Token-Zählung
Nach der Generierung führt das Skript eine automatische Qualitätsprüfung durch:
1.  Es gleicht ab, ob wirklich alle 2.457 Dateien komprimiert wurden (Soll/Ist-Vergleich).
2.  Es berechnet die genaue Wort- und geschätzte Tokenanzahl der `unified_master_digest.md`.
3.  Es prüft, ob alle Formeln korrekt formatiert sind, um mathematische Lesbarkeit im Prompt zu garantieren.

---

### Start der Umsetzung:
Ich habe diesen Fahrplan nun präzise ausgearbeitet. **Soll ich das `semantic_compressor.py`-Skript schreiben und den Kompressions- und Aggregationslauf über alle 2.457 Dateien jetzt starten?**
