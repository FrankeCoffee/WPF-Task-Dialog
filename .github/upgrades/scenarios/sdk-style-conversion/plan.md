# SDK-style Project Conversion Plan

## Overview

**Target**: Konvertierung der beiden .NET Framework 4.8 WPF-Projekte auf SDK-Style-Projektdateien ohne TFM-Änderung.
**Scope**: Kleine Lösung mit 2 Projekten und einer Projektabhängigkeit (`WPFTest` -> `TaskDialog`).

## Tasks

### 01-taskdialog-sdk: TaskDialog auf SDK-Style umstellen

`TaskDialog/TaskDialog.csproj` wird von klassischem MSBuild-Format auf SDK-Style konvertiert. Dabei bleibt das Target Framework bei `.NET Framework 4.8` (`net48`) und WPF-spezifische Einstellungen werden in das neue Projektformat übernommen. Assembly-Attribut-Generierung wird so eingestellt, dass bestehendes `AssemblyInfo.cs` keine Duplikate erzeugt.

**Done when**: `TaskDialog.csproj` nutzt SDK-Style, das Projekt baut erfolgreich, und das Ziel-Framework bleibt funktional unverändert (`net48`).

---

### 02-wpftest-sdk: WPFTest auf SDK-Style umstellen

`WPFTest/WPFTest.csproj` wird nach erfolgreicher Umstellung von `TaskDialog` in SDK-Style überführt. Die bestehende Referenz auf `TaskDialog` bleibt erhalten, WPF-Einstellungen und x86-spezifische Konfiguration werden im neuen Format korrekt abgebildet.

**Done when**: `WPFTest.csproj` nutzt SDK-Style mit intakter Projekt-Referenz zu `TaskDialog`, erfolgreichem Build und unverändertem Target Framework (`net48`).

---

### 03-solution-validation: Gesamtlösung validieren

Nach beiden Konvertierungen wird die Gesamtlösung vollständig gebaut und auf Regressionen geprüft. Es wird verifiziert, dass keine `packages.config`-Dateien verbleiben und keine unbeabsichtigte TFM-Änderung erfolgt ist.

**Done when**: Gesamtlösung baut ohne Fehler, keine `packages.config` in den konvertierten Projekten vorhanden, und beide Projekte bleiben auf `.NET Framework 4.8`.
