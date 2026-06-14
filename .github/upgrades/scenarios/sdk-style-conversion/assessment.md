# Assessment: SDK-style Conversion

## Projects to Convert
| Project | Path | packages.config | Custom Imports | Special Type | Risk |
|---------|------|----------------|----------------|-------------|------|
| TaskDialog | TaskDialog/TaskDialog.csproj | No | `$(MSBuildToolsPath)\\Microsoft.CSharp.targets` | WPF Class Library (.NET Framework 4.8) | Medium |
| WPFTest | WPFTest/WPFTest.csproj | No | `$(MSBuildToolsPath)\\Microsoft.CSharp.targets` | WPF App (.NET Framework 4.8, x86) | Medium |

## Already SDK-style (no action needed)
- none

## Baseline
- Solution builds: Yes
- Warning count: 0 (no warnings reported in latest build output)

## Key Findings
- Both projects are classic non-SDK `.csproj` files (no `Sdk` attribute, explicit file includes).
- Both projects include `Properties/AssemblyInfo.cs`; after conversion this may require `<GenerateAssemblyInfo>false</GenerateAssemblyInfo>` to avoid duplicate attributes.
- Both projects are WPF and should use `Microsoft.NET.Sdk.WindowsDesktop` with `UseWPF=true` while retaining .NET Framework targeting (`net48`).
- `WPFTest` references `TaskDialog`; conversion should follow dependency order (convert `TaskDialog` first, then `WPFTest`).
