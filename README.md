# vc-bootcamp-lerntagebuch

Lerntagebuch zum Vibecoding Bootcamp, veröffentlicht via GitHub Pages.

## Neuen Tag hinzufügen

1. `TEMPLATE.md` nach `_tage/tagX.md` kopieren (`X` = fortlaufende Nummer).
2. `title` und `date` im Front Matter anpassen.
3. Inhalt ausfüllen und committen/pushen.

Der Eintrag erscheint danach automatisch auf der Startseite (`index.md`), sortiert nach Datum.

## GitHub Pages einrichten

1. Änderungen nach GitHub pushen.
2. Im Repository unter **Settings → Pages** als Quelle **Deploy from a branch** und den Branch `main` (Ordner `/root`) auswählen.
3. Die Seite ist danach unter `https://<username>.github.io/vc-bootcamp-lerntagebuch/` erreichbar.

## Lokale Vorschau (optional)

```sh
bundle install
bundle exec jekyll serve
```

Die Seite ist dann unter `http://localhost:4000` erreichbar.
