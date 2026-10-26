# NestWurzel – GitHub Android Build

**Aktueller installierter Stand: NestWurzel 2.0.10.**

Das Repository wird erst als Build-Infrastruktur eingerichtet. Der aktuelle 2.0.10-Quellcode ist noch **nicht nachgewiesen**. Es erfolgt weder ein Release noch die Verteilung einer älteren 2.0.9 als Ersatz.

## GitHub Actions
Unter **Actions → NestWurzel Android Debug APK** lässt sich der Build manuell starten. Bei Änderungen am Quellprojekt wird er automatisch gestartet.

- **Ohne Android-Projekt:** Der Workflow erzeugt eine technisch unabhängige, separat installierbare und sichtbar als **CI-Test – KEIN NestWurzel** beschriftete APK (Paket `de.kempadesign.citest`). Artefaktname: `NUR-CI-TEST-KEINE-NestWurzel-APK`.
- **Mit vollständiger Android-Projektquelle:** Der Workflow baut `:app:assembleDebug`; auf dem Build-Rechner wird ausschließlich für Debug eine zusätzliche Paket-Endung `.ci` gesetzt, damit die aktuelle App 2.0.10 auf dem Handy nicht überschrieben werden kann. Artefaktname: `NestWurzel-QUELLSTAND-UNGEPRUEFT-CI-APK`. **Kein Nachweis, dass die Quelle 2.0.10 ist.**

Artefakte sind nach erfolgreichen Läufen im jeweiligen Actions-Lauf unter **Artifacts** als ZIP abrufbar (14 Tage).

## Vor öffentlicher Veröffentlichung
Ein echtes NestWurzel-Quellprojekt darf erst nach lokaler Prüfung auf Schlüssel, personenbezogene Daten, Kinder-/Familiendaten, private Assets, Firebase-Service-Accounts und geheime Konfigurationen hier hochgeladen werden. Nicht committen: `.env`, `local.properties`, `google-services.json`, `key.properties`, `*.keystore`, `*.jks`, `*.p12`, APKs und ZIP-Backups. `.gitignore` entfernt keine früheren Commits; automatischer Dateiscan erkennt nicht alle vertraulichen Informationen.

Benötigt werden `gradlew`, `gradle/wrapper/`, `app/`, `settings.gradle[.kts]`, Gradle-Buildskripte und die zur App gehörenden Assets. Für Projekte mit Google Services kann `google-services.json` als Base64 über das Actions-Secret `NESTWURZEL_GOOGLE_SERVICES_JSON_B64` bereitgestellt werden. Signaturschlüssel bleiben privat; Debug-Schlüssel entstehen auf dem Runner neu. Bestehende 2.0.10 niemals einfach für einen Test deinstallieren.

Die Quellstände 2.0.9/2.0.10 sind vor einer Veröffentlichung inhaltlich zu vergleichen. Die Pipeline erstellt keine Versionsnummer 2.0.11 und keine Release-APK.