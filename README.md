# J.A.R.V.I.S. für Android

Persönlicher KI-Assistent als native Android-App (Kotlin, Jetpack Compose) mit Python/FastAPI-Backend und Claude als KI-Modell.

## Stand

- [x] Designkonzept „Der Kern“: [`docs/design/DESIGN-KONZEPT.md`](docs/design/DESIGN-KONZEPT.md)
- [x] Animations-Prototyp: `docs/design/jarvis-core-prototyp.html` (im Browser öffnen)
- [ ] Phase 1: Android-Grundgerüst
- [ ] Phase 2: Sprachsteuerung
- [ ] Phase 3: KI-Anbindung (Backend)
- [ ] Phase 4: Smartphone-Aktionen
- [ ] Phase 5: Gedächtnis
- [ ] Phase 6: Aktivierungswort / Hintergrundbetrieb
- [ ] Phase 7: Release-APK

## Sicherheit

API-Schlüssel gehören **nie** in die App oder ins Repository. Sie liegen nur im Backend als Umgebungsvariable (`.env`, per `.gitignore` ausgeschlossen).
