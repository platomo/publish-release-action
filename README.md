
# Publish Release

Diese GitHub-Action löscht optional alte Veröffentlichungen und erstellt eine neue Veröffentlichung für ein angegebenes Paket.

## Beschreibung

Diese Action bietet eine Möglichkeit, eine neue Version eines Pakets zu veröffentlichen, indem sie eine alte Version löscht (falls konfiguriert) und eine neue erstellt. Optional kann die Veröffentlichung als Entwurf oder Vorabversion markiert werden.

## Eingaben

| Name              | Beschreibung                                         | Erforderlich | Standardwert |
|-------------------|------------------------------------------------------|--------------|--------------|
| `package-version` | Die Versionsnummer des Pakets, das veröffentlicht wird | Ja           | Keine        |
| `delete-existing` | Gibt an, ob bestehende Veröffentlichungen gelöscht werden sollen | Nein          | Keine        |
| `pre-release`     | Gibt an, ob es sich um eine Vorabversion handelt      | Nein          | Keine        |
| `py-version`      | Die Python-Version, die für die Tests verwendet wird  | Ja           | Keine        |

## Verwendung

Erstellen Sie eine Workflow-Datei (z. B. `.github/workflows/release.yml`) und verwenden Sie diese Action wie folgt:

```yaml
name: Publish New Release

on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  release:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Publish Release
        uses: platomo/publish-release-action@main
        with:
          package-version: "1.0.0"
          delete-existing: true
          pre-release: false
          py-version: "3.9"
```

## Schritte im Workflow

1. **Bestehende Veröffentlichung löschen** (optional): Löscht die vorhandene Veröffentlichung und das zugehörige Tag, falls `delete-existing` auf `true` gesetzt ist.
2. **Veröffentlichung erstellen und Assets hochladen**: Erstellt die neue Veröffentlichung und lädt alle Dateien im `dist/`-Ordner hoch.
3. **Veröffentlichung als Entwurf markieren** (optional): Markiert die Veröffentlichung als Entwurf, wenn `draft-release` auf `true` gesetzt ist.
4. **Vorabversion festlegen** (optional): Setzt die Veröffentlichung als Vorabversion, wenn `pre-release` auf `true` gesetzt ist.

## Erforderliche Berechtigungen

Diese Action benötigt ein GitHub-Token (`GH_TOKEN`), das automatisch im Workflow-Umfeld zur Verfügung steht, um die Veröffentlichung zu erstellen und zu bearbeiten.

