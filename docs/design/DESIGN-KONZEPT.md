# J.A.R.V.I.S. – Designkonzept „Der Kern“

Stand: Entwurf v1, wartet auf Feedback. Zum Ansehen: `jarvis-core-prototyp.html` im Browser öffnen
(Tasten 1–6 = Zustände, `d` = Demo-Ablauf, oder aufs Mikrofon tippen).

## Leitidee

Du sprichst nicht mit einer App, du sprichst mit **JARVIS**. Deshalb besteht der Bildschirm im Kern aus genau einem Ding:
einer holografischen Partikelkugel. Alles andere ist so klein und leise, dass man es kaum bemerkt.

Orientierung: Referenz 1 (orange-goldene Partikelstruktur), aber stark reduziert. Aus Referenz 2 übernehme ich nur
die Idee feiner, kreisförmiger HUD-Linien.

## Was auf dem Bildschirm ist (vollständige Liste)

| Element | Position | Zweck |
|---|---|---|
| Partikelkern | Mitte, ca. 60 % der Breite | Identität und Zustandsanzeige |
| „J.A.R.V.I.S.“ | im Zentrum des Kerns, sehr dezent | Name |
| 3 feine HUD-Ringe + Skala | um den Kern | Technik-Look, reagieren auf Zustand |
| Statuswort | oben, winzig, gesperrt | z. B. STANDBY / HÖRE ZU |
| eine Textzeile | unter dem Kern, nur bei Bedarf | erkannter Satz oder Kurzantwort |
| Mikrofon-Ring | unten | Push-to-Talk |

Mehr gibt es nicht: keine Karten, keine Widgets, keine Navigationsleiste. Einstellungen und Gedächtnis kommen
später auf eigene, genauso reduzierte Seiten (z. B. per Wischgeste erreichbar).

## Farben

- Hintergrund: reines Schwarz `#000000` (spart auf OLED-Displays auch Akku)
- Gold `#FFA84E`: Standardfarbe der Partikel
- Kernlicht `#FFF4DE`: hellste Partikel, Zentrum
- Weißgold `#FFE2B0`: Aktion wird ausgeführt
- Rot `#FF482C`: Fehler

## Zustände

| Zustand | Verhalten des Kerns |
|---|---|
| IDLE | langsamer Wirbel, ruhiges Glimmen |
| LISTENING | Kern dehnt sich leicht, Rand verformt sich wellenförmig mit dem Mikrofonpegel, Außenring leuchtet mit |
| THINKING | Kern zieht sich zusammen, Partikel beschleunigen und ziehen lange Leuchtspuren, Scanner-Bogen kreist |
| SPEAKING | Kern und Zentrum pulsieren im Rhythmus der Sprachausgabe |
| EXECUTING_ACTION | Farbe wird weißgold, ein Fortschrittsbogen läuft einmal um den Kern |
| ERROR | rot, gedimmt, unruhiges Flackern, HUD-Skala „bricht“ stellenweise |

Übergänge zwischen den Zuständen sind weich (alle Parameter werden interpoliert), es gibt keine harten Schnitte.

## Technische Übertragbarkeit auf Android (ehrliche Einschätzung)

Den Prototyp habe ich bewusst so gebaut, dass er sich 1:1 nach Jetpack Compose übertragen lässt:

- `Canvas` + `drawLine`/`drawCircle`/`drawArc` mit `BlendMode.Plus` (additives Leuchten)
- Nachleuchten der Partikel: in Compose gibt es kein „halbtransparent übermalen“ wie im Browser. Ich würde stattdessen
  pro Partikel die letzten Positionen speichern und als kurze Linie zeichnen. Das sieht gleich aus und ist sauberer.
- Animation über `withFrameNanos` in einem `LaunchedEffect`
- Mikrofonpegel kommt später aus `SpeechRecognizer` (`onRmsChanged`), der Sprechpuls aus dem
  `TextToSpeech`-Fortschritt. Im Prototyp sind beide Signale simuliert.
- Performance: ca. 1.600 Partikel. Auf aktuellen Mittelklasse-Geräten sollte das flüssig laufen. Das ist eine Schätzung,
  erst ein Test auf deinem Gerät zeigt es sicher. Notfalls reduzieren wir die Partikelzahl.

## Offene Fragen an dich

1. Passt die Grundrichtung (goldener Partikelkern, Rest fast unsichtbar)?
2. Kern größer, kleiner oder genau richtig?
3. Statuswort oben und Textzeile unten: behalten oder noch weiter reduzieren?
4. Anrede in den Antworten: „Sie“ (wie im Film-Deutsch) oder „du“?
