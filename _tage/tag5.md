---
title: "Tag 5"
date: 2026-09-04
---

## Was ich heute gelernt habe

- Konsolenprogramme haben zwei Zielgruppen: Menschen brauchen hilfreiche Erklärungen, Skripte dagegen möglichst klare und maschinenlesbare Ausgaben. Deshalb kann der QUIQQER-Header bei `./console` und `./console --help` sichtbar bleiben, sollte bei konkreten Befehlen aber nicht den eigentlichen Output überdecken.
- Verlässliche Automatisierung braucht definierte Exit-Codes. Beim Passwort-Reset unterscheiden die Codes nun Erfolg (`0`), Laufzeitfehler (`1`), nicht gefundene Benutzer:innen (`2`) und Abbruch (`3`). Ein aufrufendes Skript kann dadurch gezielt reagieren, ohne Textmeldungen parsen zu müssen.
- Ein CLI-Befehl wird robuster, wenn er fachlich eindeutige Identifikatoren akzeptiert. Der Passwort-Reset kann Benutzer:innen deshalb sowohl über den Benutzernamen als auch über die UUID auflösen und zeigt vor der Bestätigung beide Werte an.
- Nicht-interaktive Befehle müssen Sicherheit und Automatisierbarkeit zusammenbringen: Passwörter können über `stdin` übergeben werden, und generierte Passwörter dürfen nicht in Fehlermeldungen oder Logs landen.
- Prozessisolation in PHPUnit schützt vor gemeinsamem globalem Zustand, kann Test-Fixtures aber sehr teuer machen. Läuft jede Testmethode in einem eigenen Prozess, können statische Helper ein bereits erzeugtes Testprojekt nicht wiederverwenden. Eine Isolation pro Testklasse kann die Zahl vollständiger Projektinitialisierungen deutlich reduzieren.
- Unit-Tests sollten keine echten Downloads ausführen. Dependency Injection und Fakes machen solche Tests schneller, deterministischer und verhindern, dass ein Test versehentlich den installierten Composer-PHAR verändert.
- Laufzeitmessungen helfen, an der richtigen Stelle zu optimieren: In der untersuchten Suite entfielen 93,4 % der Laufzeit auf Integrationstests und 81,7 % auf prozessisolierte Tests mit Projekt-Fixture. Wenige langsame Tests bestimmten damit fast die gesamte Feedbackzeit.

## Was ich gebaut / ausprobiert habe

- Den erweiterten Passwort-Reset aus [QUIQQER Core !550](https://dev.quiqqer.com/quiqqer/core/-/merge_requests/550) nach erfolgreicher Pipeline in `next-2.x` übernommen und das zugehörige [Issue #1550](https://dev.quiqqer.com/quiqqer/core/-/work_items/1550) abgeschlossen.
- Für [Issue #1552](https://dev.quiqqer.com/quiqqer/core/-/work_items/1552) die Sichtbarkeitsregel des Konsolen-Headers umgesetzt, mit acht gezielten Unit-Tests sowie einem Laufzeittest geprüft und über [Merge Request !555](https://dev.quiqqer.com/quiqqer/core/-/merge_requests/555) gemergt.
- Die Performance-Analyse der PHPUnit-Suite in [Issue #1553](https://dev.quiqqer.com/quiqqer/core/-/work_items/1553) diskutiert und insbesondere hinterfragt, wo Prozessisolation pro Testmethode wirklich erforderlich ist.

## Herausforderungen

- Die Konsolenausgabe gleichzeitig angenehm für Menschen und stabil für automatisierte Skripte zu gestalten.
- Tests zu beschleunigen, ohne die Isolation unkontrolliert abzuschwächen: globale und statische Zustände, Sessions, Berechtigungs-Caches sowie erzeugte Dateien und Daten müssen zuverlässig zurückgesetzt werden.
- Bei der Validierung zwischen Fehlern der eigenen Änderung und bereits vorhandenen, reproduzierbaren Testfehlern zu unterscheiden.

## Nächste Schritte

- Die betroffenen Tests zunächst auf Prozessisolation pro Klasse umstellen und mit mehreren vergleichbaren Läufen messen, wie stark sich die Gesamtlaufzeit verbessert.
- Prüfen, welche Testklassen ganz ohne Prozessisolation stabil laufen, und dafür alle veränderlichen Zustände explizit zurücksetzen.
- Den echten Composer-Download aus der Unit-Suite entfernen und schnelle Unit-Tests klar von der vollständigen Integrationstest-Suite trennen.
