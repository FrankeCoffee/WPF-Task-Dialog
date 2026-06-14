# 02-wpftest-sdk: WPFTest auf SDK-Style umstellen

`WPFTest/WPFTest.csproj` wird nach erfolgreicher Umstellung von `TaskDialog` in SDK-Style überführt. Die bestehende Referenz auf `TaskDialog` bleibt erhalten, WPF-Einstellungen und x86-spezifische Konfiguration werden im neuen Format korrekt abgebildet.

## Research Findings

### Projects Affected
- `WPFTest/WPFTest.csproj` — direktes Zielprojekt dieser Aufgabe
- `TaskDialog/TaskDialog.csproj` — Referenzprojekt, muss nach Konvertierung weiter korrekt aufgelöst werden

### Files to Modify
- `WPFTest/WPFTest.csproj` — Konvertierung auf SDK-Style und Beibehaltung der Projektabhängigkeit

### Dependencies & Risks
- WPF-Projekt benötigt `Microsoft.NET.Sdk.WindowsDesktop` + `UseWPF=true`
- Plattformkonfiguration `x86` muss erhalten bleiben
- Projekt-Referenz auf `TaskDialog` darf nicht verloren gehen
- Target Framework muss bei `net48` bleiben

### Decisions Made
- Konvertierung mit `convert_project_to_sdk_style` (Tool-basiert, keine manuelle Neuerstellung)
- Build-Validierung per Projektbuild via MSBuild

**Done when**: `WPFTest.csproj` nutzt SDK-Style mit intakter Projekt-Referenz zu `TaskDialog`, erfolgreichem Build und unverändertem Target Framework (`net48`).
