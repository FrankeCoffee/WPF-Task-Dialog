# 03-solution-validation: Gesamtlösung validieren

Nach beiden Konvertierungen wird die Gesamtlösung vollständig gebaut und auf Regressionen geprüft. Es wird verifiziert, dass keine `packages.config`-Dateien verbleiben und keine unbeabsichtigte TFM-Änderung erfolgt ist.

**Done when**: Gesamtlösung baut ohne Fehler, keine `packages.config` in den konvertierten Projekten vorhanden, und beide Projekte bleiben auf `.NET Framework 4.8`.
