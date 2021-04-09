# Automatische Formattierung mit Prettier

Die automatische Integration von `Prettier` in den Git-Prozess stellt sicher, dass sämtlicher geänderter Code noch vor dem Commit einheitlich formatiert wird. 

## Voraussetzungen

- **Prettier** ist im Projekt [installiert und konfiguriert](tools/prettier.md).

## Installation

Für die automatische Formatierung von geänderten/gestagten Dateien werden die Pakete [`husky`](https://github.com/typicode/husky) und [`pretty-quick`](https://github.com/azz/pretty-quick) benötigt. Mit `Husky` können verschiedenen Git-Hooks verwendet werden (z.B. Commit, Push). `Pretty-Quick` wiederum führt die `Prettier`-Formatierung auf den geänderten Dateien durch.

```bash
npm install pretty-quick husky --save-dev
```

## Konfiguration

Für die Konfiguration muss `Husky` initialisiert und der entsprechende Hook bzw. Befehl anschliessend hinzugefügt werden.

```bash
npx husky install
npx husky add .husky/pre-commit "npx pretty-quick --staged"
```

Beim Commiten werden fortan sätmliche relevanten geänderten Dateien mit `Prettier` automatisch formatiert, was auch in der Konsole sichtbar ist.

```
git commit -m "Update"
🔍  Finding changed files since git revision b9f43f3.
🎯  Found 3 changed files.
✍️  Fixing up uimodule/webapp/controller/BaseController.js.
✅  Everything is awesome!
[main d0f6fc5] Update
 4 files changed, 18 insertions(+), 20 deletions(-)
 create mode 100644 .husky/pre-commit
```