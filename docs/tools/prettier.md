# Prettier

[`Prettier`](https://prettier.io/) ist ein Code Formatierungs-Werkzeug. Die Verwendung von `Prettier` stellt sicher, dass der Code für alle Entwickler einheitlich formatiert ist.

## Installation

Nebst `Prettier` muss zusätzlich eine Konfiguration für `ESLint` installiert werden. Diese Konfiguration stellt sicher, dass alle Regeln hinsichtlich der durch `Prettier` vorgenommenen Formatierung in `ESLint` deaktiviert werden. Die Verwendung dieser Regeln erfolgt in der [Konfiguration von `ESLint`](tools/eslint.md#konfiguration).

```bash
npm install prettier --save-dev --save-exact
npm install eslint-config-prettier --save-dev
```

> Der Parameter --save-exact ist für `prettier` **zwingend** zu verwenden, da Prettier auch in Minor-Versionen die Formattierung verändern kann und so ein automatisches Update verhindert wird.

## Konfiguration

Die Konfiguration erfolgt mit der Datei `.prettierrc`. Mit Ausnahme der untenstehenden Regel werden die [Standardregeln](https://prettier.io/docs/en/options.html) angewendet.

```json
{
  "singleQuote": true,
  "endOfLine": "auto"
}
```

Die Formatierung kann mit Hilfe der Datei `.prettierignore` für Dateien und Verzeichnisse deaktiviert werden. In der Regel sollten generierte Artifakte nicht automatisch formatiert werden, wobei solche normalerweise auch nicht über ein Repository verwaltet werden und somit keine [automatische Formatierung beim Commit](git/prettier.md) forciert wird.

```text
dist
...
```

## Verwendung

`Prettier` wird in der Regel manuell, spätestens jedoch beim [Commit](git/prettier.md) ausgeführt.

Um zu verhindern, dass bestimmte Code-Zeilen formatiert werden, kann folgender Kommentar vor die entsprechende Zeile gestellt werden.

```javascript
// prettier-ignore
```