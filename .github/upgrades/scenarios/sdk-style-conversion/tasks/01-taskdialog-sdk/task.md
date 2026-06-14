# 01-taskdialog-sdk: TaskDialog auf SDK-Style umstellen

`TaskDialog/TaskDialog.csproj` wird von klassischem MSBuild-Format auf SDK-Style konvertiert. Dabei bleibt das Target Framework bei `.NET Framework 4.8` (`net48`) und WPF-spezifische Einstellungen werden in das neue Projektformat übernommen. Assembly-Attribut-Generierung wird so eingestellt, dass bestehendes `AssemblyInfo.cs` keine Duplikate erzeugt.

## Research Findings

### Projects Affected
- `TaskDialog/TaskDialog.csproj` — direktes Zielprojekt dieser Aufgabe (WPF Library)
- `WPFTest/WPFTest.csproj` — indirekt betroffen als Referenzverbraucher (Build-Verifikation nachgelagert)

### Files to Modify
- `TaskDialog/TaskDialog.csproj` — Projektformat-Konvertierung nach SDK-Style

### Dependencies & Risks
- WPF erfordert `Microsoft.NET.Sdk.WindowsDesktop` und `UseWPF=true` im SDK-Style-Projekt
- Vorhandenes `Properties/AssemblyInfo.cs` kann doppelte Assembly-Attribute erzeugen; `GenerateAssemblyInfo` muss deaktiviert werden
- Target Framework darf nicht verändert werden (muss `net48` bleiben)

### Decisions Made
- Konvertierung erfolgt mit dem dedizierten Tool `convert_project_to_sdk_style` (keine manuelle XML-Neuerstellung)
- Build-Validierung erfolgt projektspezifisch für `TaskDialog` mit MSBuild wegen WPF/.NET Framework

**Done when**: `TaskDialog.csproj` nutzt SDK-Style, das Projekt baut erfolgreich, und das Ziel-Framework bleibt funktional unverändert (`net48`).
