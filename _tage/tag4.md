---
title: "Tag 4"
date: 2026-09-03
---

## Was ich heute gelernt habe

- **Lokale Entwicklung vs. Produktion:** Beim lokalen Start wird ein Webserver auf dem eigenen Rechner gestartet, die App gebaut und unter `localhost:3000` im Browser ausgeliefert – sichtbar ist das aber nur für mich selbst.
- **Warum ein lokaler Server nicht reicht:** keine feste öffentliche Adresse (Domain/IP), läuft nicht 24/7, Sicherheitsrisiko durch Fremde im eigenen Netz, begrenzter Upload und vom Provider gesperrte Ports.
- **Hosting-Anbieter lösen genau diese Probleme:** feste Adresse, 24/7-Verfügbarkeit, gesondertes Netzwerk und (fast) kein Konfigurationsaufwand. Schöner Merksatz aus der Session: „There is no cloud – it's just someone else's computer."
- **Push-based Deployment:** Code wird gepusht, ein neuer Build startet, der vorherige Produktionsstand wird ersetzt.
- **Mehrere Umgebungen** verhindern, dass ein fehlerhafter Stand live geht: eine Umgebung pro Feature, Features gebündelt auf „Staging", nur fertige und abgenommene Stände auf „Produktion".
- **PaaS (Platform as a Service):** Plattform für technische Infrastruktur, die die Anwendung dauerhaft erreichbar macht und Wartung sowie Sicherheit der Infrastruktur übernimmt.
- **Die vier vorgestellten Anbieter im Vergleich:**
  - *Vercel* – „von und für" Next.js, automatisches Deployment via GitHub, kostenloser Plan, Serverless Functions für leichte Backend-Arbeit, Preview-Deployments pro Pull Request. Am besten für Next.js/React und statische Seiten.
  - *Netlify* – framework-agnostisch, funktioniert mit allem, was HTML/CSS/JS ausgibt; Deployment via GitHub oder Drag & Drop im Dashboard, Preview-Deployments, Extras wie Formulare, A/B-Testing und Identity-Service. Am besten für statische Seiten wie Portfolios und Landing Pages.
  - *Railway* – echter Server mit laufenden Prozessen statt nur statischer Dateien, Datenbanken lassen sich einfach ergänzen, Preview-Deployments müssen aktiviert werden, kostenloser Plan stark begrenzt (derzeit ca. 5 $/Monat). Am besten für Full-Stack-Apps, APIs und Chatbots.
  - *Replit* – kein Setup nötig, alles läuft im Browser, 1-Klick-Deployment, Live-Multiplayer-Sessions; Preismodell variiert stark und ist etwas undurchsichtig. Am besten für Prototypen, Demos und schnelle Experimente.
- **Eigener Server (VPS/Dedicated)** gibt volle Kontrolle, bedeutet aber deutlich mehr Aufwand bei Setup und Wartung – die gesamte Infrastruktur liegt in der eigenen Verantwortung. Anbieter z. B. Hetzner oder Strato.
- **Entscheidungshilfe:** Nur Frontend mit Next.js → Vercel, anderes Frontend → Netlify, schnell testen ohne lokales Setup → Replit, Backend/Datenbank → Railway (managed) oder VPS (selbst). Im Zweifel mit Vercel oder Netlify starten; VPS nur mit Linux-Erfahrung.
- **Logs sind das Tagebuch der App.** Typische HTTP-Statuscodes: `200 OK` (Anfrage erfolgreich), `301 Moved Permanently` (Ressource umgezogen, Browser folgt der Weiterleitung), `404 Not Found` (Ressource existiert nicht, falsche URL oder fehlende Route), `5xx Server Error` (etwas im Code ist kaputt – Alarmsignal, Logs checken).
- **Typische Fehler nach dem Deployment:**
  - *Build-Fehler* – Deployment schlägt fehl, die alte Version bleibt online, die Ursache steht in den Logs.
  - *Dependency-Probleme* – lokal läuft alles, auf dem Server nicht; oft wegen unterschiedlicher Versionen (node, npm, …).
  - *Fehlende Umgebungsvariablen* – die App startet, funktioniert aber trotzdem nicht; ein Blick in die Dev-Tools hilft.

## Was ich gebaut / ausprobiert habe

- Ein Projekt selbst deployt, die Logs des Anbieters gelesen und die Fehler im Zyklus Deploy – Debug – Re-Deploy behoben.

## Herausforderungen

-

## Nächste Schritte

-
