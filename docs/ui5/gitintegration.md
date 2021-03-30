# Git Integration

Die automatische Integration von `Prettier` in den Git-Prozess stellt sicher, dass sämtlicher Code noch vor dem Commit einheitlich formatiert wird.

> Die Installation und Konfiguration der notwendigen Komponenten erfolgt entweder direkt in den einzelnen Apps oder im Falle von Multitarget-Anwendungen im Wurzelverzeichnis.

## Husky & Pretty-Quick

Für die automatische Formattierung von geänderten/gestageten Dateien werden die Pakete `husky` und `pretty-quick` benötigt. Mit `Husky` können verschiedenen Git-Hooks verwendet werden (z.B. Commit, Push). `Pretty-Quick` wiederum führt die `Prettier`-Formatierung auf den geänderten Dateien durch.

### Installation

```bash
npm install pretty-quick husky --save-dev
```

### Konfiguration

Nach der Installation kann in der `package.json` Datei der durch `Husky` bereitgestellte Hock `Prettier` ausgefüht werden.

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
