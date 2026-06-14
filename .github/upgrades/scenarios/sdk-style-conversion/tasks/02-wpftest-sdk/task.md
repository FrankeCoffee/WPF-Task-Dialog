# 02-wpftest-sdk: WPFTest auf SDK-Style umstellen

`WPFTest/WPFTest.csproj` wird nach erfolgreicher Umstellung von `TaskDialog` in SDK-Style überführt. Die bestehende Referenz auf `TaskDialog` bleibt erhalten, WPF-Einstellungen und x86-spezifische Konfiguration werden im neuen Format korrekt abgebildet.

**Done when**: `WPFTest.csproj` nutzt SDK-Style mit intakter Projekt-Referenz zu `TaskDialog`, erfolgreichem Build und unverändertem Target Framework (`net48`).
