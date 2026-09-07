---
title: "Tag 6"
date: 2026-09-07
---

## Was ich heute gelernt habe

*Das Wochenende wird im Lerntagebuch übersprungen; Tag 6 entspricht Montag, dem 7. September. Diese Inhalte habe ich nicht im Vibecoding Bootcamp, sondern während meiner beruflichen Arbeit gelernt.*

- Eine grüne Unit-Test-Suite beweist noch nicht, dass sich eine Anwendung vollständig installieren lässt. Ein automatisierter Installations-Smoke-Test prüft den tatsächlichen Ablauf mit Paketen, Datenbank und Laufzeitumgebung und erkennt dadurch Integrationsprobleme vor einem Release.
- Solche Smoke-Tests entfalten den größten Nutzen an den richtigen Auslösern: vor einer neuen Installer-Version und beim Erstellen der QUIQQER-Docker-Images. Schlägt eine Installation fehl, sollte die verantwortliche Person direkt benachrichtigt werden.
- Eine Supportmatrix ist auch eine Produktentscheidung. Für PostgreSQL wurde festgelegt, zunächst nur die jeweils neueste Version zu unterstützen. Das begrenzt Testaufwand und Variantenvielfalt, muss aber klar dokumentiert und durch die CI abgebildet werden.
- Öffentliche APIs sollten möglichst keine Objekte externer Bibliotheken zurückgeben. Andernfalls wird deren API Teil des eigenen Vertrages und ein Update der Abhängigkeit kann bei Aufrufern unerwartete Breaking Changes verursachen.
- Eine eigene Facade kapselt die externe Bibliothek und stabilisiert den Vertrag. Für eine schrittweise Migration kann ein Intersection Return Type ausdrücken, dass ein Objekt vorübergehend sowohl den neuen QUIQQER-Vertrag als auch den bisherigen Bibliothekstyp erfüllt; das funktioniert jedoch nur, wenn das konkrete Objekt tatsächlich beide Typen implementiert.
- GitLab-Jobs derselben Stage können parallel laufen, solange keine Abhängigkeit sie künstlich serialisiert. Wird PHPStan wie PHPUnit in die Stage `test` eingeordnet, muss PHPUnit nicht mehr auf die statische Analyse warten und die kritische Pipeline-Laufzeit kann sinken.
- Änderungen an wiederverwendbaren CI-Komponenten sollten zuerst in einem Verbraucherprojekt gegen den Feature-Branch getestet werden. Erst danach wird die Komponente nach `main` übernommen und in weitere Entwicklungslinien wie `next-4.x` weitergeführt.

## Was ich gebaut / ausprobiert habe

- Den Stand der automatisierten QUIQQER-Installationsprüfungen bewertet und [Core-Issue #1188](https://dev.quiqqer.com/quiqqer/core/-/work_items/1188) geschlossen, weil Installer-Releases und Docker-Image-Builds inzwischen reale Installationen ausführen und Fehler melden.
- Die Entscheidung dokumentiert, bei PostgreSQL vorerst nur die neueste Version zu unterstützen ([Core-Issue #1541](https://dev.quiqqer.com/quiqqer/core/-/work_items/1541)).
- Die Einführung einer QUIQQER-eigenen Image-Manager-Facade und einen kompatiblen Übergang über Intersection Types diskutiert ([Core-Issue #1506](https://dev.quiqqer.com/quiqqer/core/-/work_items/1506)).
- In der Package-Bundle-Komponente PHPStan über den vorhandenen Input `job-stage` in die Stage `test` verschoben, die Änderung in `quiqqer/test` gegen `next-3.x` in einer [erfolgreichen Pipeline](https://dev.quiqqer.com/quiqqer/test/-/pipelines/31927) erprobt und über [Merge Request !48](https://dev.quiqqer.com/quiqqer/stabilization/ci-cd-components/quiqqer-package-bundle/-/merge_requests/48) nach `main` übernommen.
- Den neuen Stand über [Merge Request !49](https://dev.quiqqer.com/quiqqer/stabilization/ci-cd-components/quiqqer-package-bundle/-/merge_requests/49) nach `next-4.x` übertragen und das zugehörige [Issue #28](https://dev.quiqqer.com/quiqqer/stabilization/ci-cd-components/quiqqer-package-bundle/-/work_items/28) abgeschlossen.

## Herausforderungen

- Installations-Smoke-Tests so in Release- und Image-Pipelines einzubinden, dass Fehler früh sichtbar werden und eindeutig einem auslösenden Stand zugeordnet werden können.
- Den Nutzen einer kleineren Datenbank-Supportmatrix gegen die Anforderungen bestehender Installationen abzuwägen.
- Eine externe Bibliothek hinter einer eigenen Facade zu kapseln, ohne den bisherigen API-Vertrag abrupt zu brechen.
- CI-Jobs zu parallelisieren, ohne notwendige Artefakt- oder Reihenfolgeabhängigkeiten zu übersehen.

## Nächste Schritte

- Die tatsächliche Pipeline-Laufzeit vor und nach der Parallelisierung von PHPStan und PHPUnit vergleichen.
- Die Image-Manager-Facade prototypisch umsetzen und prüfen, ob der Intersection Return Type den bestehenden Aufrufervertrag in der Übergangsphase erfüllt.
- Die PostgreSQL-Unterstützung in Dokumentation und Testmatrix eindeutig auf die jeweils unterstützte Version begrenzen.
