---
title: "Tag 3"
date: 2026-09-02
---

## Was ich heute gelernt habe

*Diese Inhalte habe ich nicht im Vibecoding Bootcamp, sondern während meiner beruflichen Arbeit gelernt.*

- Ein Import sollte unsichere Eingaben vollständig prüfen, bevor er den Zielzustand verändert. Bei Dateisystemarchiven reicht es nicht, erst während des Entpackens auf problematische Inhalte zu reagieren.
- TAR-Archive können neben regulären Dateien und Verzeichnissen auch symbolische Links oder andere spezielle Einträge enthalten. Solche Einträge müssen vor der Extraktion erkannt und abgelehnt werden, damit sie nicht aus dem vorgesehenen Zielverzeichnis herausführen oder unerwartete Dateitypen erzeugen.
- Fehlermeldungen sind besonders hilfreich, wenn sie nicht nur „ungültiges Archiv“ melden, sondern alle gefundenen problematischen Einträge benennen. Dafür kann die Validierung zunächst die Treffer sammeln beziehungsweise zählen und erst nach dem vollständigen Prüflauf abbrechen.
- CLI-Dokumentation sollte genau erklären, wie Eingabepfade aufgelöst werden. Der QUIQQER-Import akzeptiert relative und absolute Pfade; relative Pfade beziehen sich auf das Verzeichnis, in dem der Befehl aufgerufen wird.
- Prozessisolierte PHPUnit-Tests benötigen eine klar geregelte Eigentümerschaft für globale Aufräumarbeiten. Registriert auch ein Kindprozess den zentralen Cleanup-Handler, kann er gemeinsam verwendete Testprojekte zu früh entfernen.
- Die Prozess-ID des ursprünglichen Testprozesses lässt sich in einer Umgebungsvariable festhalten. So kann jeder Prozess feststellen, ob er für die globale Bereinigung zuständig ist, während ein isolierter Kindprozess nur seine eigenen lokalen Fixtures aufräumt.
- Ein gezielter Regressionstest mit `RunInSeparateProcess` und deaktivierter Übernahme des globalen Zustands kann sicherstellen, dass ein Kindprozess den globalen Cleanup nicht registriert.

## Was ich gebaut / ausprobiert habe

- Im QUIQQER-DDEV-Import werden bei einer Ablehnung jetzt alle nicht unterstützten Archiveinträge ausgegeben. Ein Acceptance-Test erzeugt dazu gezielt ein Archiv mit mehreren symbolischen Links und prüft, dass der Import ohne Änderungen am Ziel abbricht ([Commit `6b78c725`](https://dev.quiqqer.com/quiqqer/ecosystem/ddev/-/commit/6b78c7254c4aa438e98ab1d164afb2d05aae2380)).
- Die Import-Dokumentation um ein konkretes Beispiel mit relativen Pfaden und eine Erklärung zur Pfadauflösung ergänzt ([Commit `563e5544`](https://dev.quiqqer.com/quiqqer/ecosystem/ddev/-/commit/563e5544b6ce1efcfcbd8e4abb70446840448f11)).
- In QUIQQER Core einen neuen Arbeitsbranch für den verbesserten Passwort-Reset angelegt und dabei eine Änderung zur Testbereinigung übernommen: Der globale Cleanup ist auf den ursprünglichen Prozess begrenzt, das lokale Projekt-Cleanup wird separat registriert und das Verhalten ist mit einem isolierten Test abgesichert. Die zugehörige Pipeline war erfolgreich ([Commit `1aeeebd4`](https://dev.quiqqer.com/quiqqer/core/-/commit/1aeeebd48aead869700f3313d6f5dffb68aa59b0)).

## Herausforderungen

- Sicherheitsprüfungen so früh auszuführen, dass ein ungültiger Import garantiert keine Datenbank-, Datei- oder Konfigurationsänderungen hinterlässt.
- Fehlerausgaben zugleich kompakt und konkret genug zu gestalten, damit sich ein problematisches Archiv ohne weitere Diagnose untersuchen lässt.
- Bei prozessisolierten Tests zwischen globaler Bereinigung durch den Hauptprozess und lokaler Bereinigung innerhalb eines Kindprozesses zu unterscheiden.

## Nächste Schritte

- Die Import-Validierung um weitere ungewöhnliche Archivtypen und negative Testfälle ergänzen.
- Die Cleanup-Logik mit mehreren aufeinanderfolgenden und parallel isolierten Testprozessen beobachten.
- Weiter dokumentieren, welche Pfade und Zustände ein fehlgeschlagener Import bewusst unverändert lässt.
