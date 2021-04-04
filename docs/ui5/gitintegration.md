# Automatische Formattierung mit Git

Die automatische Integration von `Prettier` in den Git-Prozess stellt sicher, dass sämtlicher Code noch vor dem Commit einheitlich formatiert wird. Für die automatische Formatierung von geänderten/gestagten Dateien werden die Pakete [`husky`](https://github.com/typicode/husky) und [`pretty-quick`](https://github.com/azz/pretty-quick) benötigt. Mit `Husky` können verschiedenen Git-Hooks verwendet werden (z.B. Commit, Push). `Pretty-Quick` wiederum führt die `Prettier`-Formatierung auf den geänderten Dateien durch.

> Die Installation und Konfiguration der notwendigen Komponenten erfolgt entweder direkt in den einzelnen Apps oder im Falle von Multitarget-Anwendungen im Wurzelverzeichnis.

## Installation

```bash
npm install pretty-quick husky --save-dev
```

## Konfiguration

Nach der Installation kann in der `package.json` der durch `Husky` bereitgestellte Hook für `pretty-quick` `Prettier` werden.

```json
{
  ...
  "husky": {
    "hooks": {
      "pre-commit": "pretty-quick --staged"
    }
  }
}
```
