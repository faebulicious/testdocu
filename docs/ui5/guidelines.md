# Coding Guidelines

Mit Hilfe von Coding Guidelines kann die Code Qualität erhöht werden. Gleichzeitig vereinfacht einheitliches Coding die Wartung und verkürzt das Onboarding von neuen Entwicklern. Allerdings nützen umfangreiche Regelwerke nichts, wenn nicht sichergestellt wird, dass sich alle an diese Regeln halten. 

Mit Hilfe von statischer Code Analyse ist es möglich, den Code gegen ein vordefiniertes Regelwerk zu prüfen. Die zusätzliche, separate Dokumentation des Regelwerks entfällt, da dieses bereits durch das entsprechende Werkzeug ausreichend dokumentiert ist.

Ebenfalls wichtig für die Zusammenarbeit an Code sind einheitliche Formatierungen. Entwickler haben sich zwar oft eigene "Best-Practices" angeeignet, ein gemeinsamer Konsens ist aber unverzichtbar.

Für die statische Code-Analyse eignet sich [`ESLint`](https://eslint.org/) im Zusammenspiel mit der weit verbreiteten Konfiguration von [`Airbnb`](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb) sowie [`Prettier`](https://prettier.io/) für die einheitliche Formatierung.

## Installation

```bash
npm install prettier --save-dev --save-exact
npm install eslint eslint-config-prettier eslint-config-airbnb-base --save-dev
```

> Der Parameter --save-exact ist für `prettier` **zwingend** zu verwenden, da Prettier auch in Minor-Versionen die Formattierung verändern kann und so ein automatisches Update verhindert wird.

## Konfiguration

Die Konfiguration kann für ESLint und Prettier in verschiedenen Dateiformaten und -namen erfolgen. Grundsätzlich soll die Konfiguration mittels `json` und der Dateiendung `.json` erfolgen.

Die nachfolgenden Konfigurationsdateien können innerhalb eines Projekts mehrfach vorhanden sind, um für unterschiedliche Artifakte unterschiedliche Konfiguration zu ermöglichen. Dies ist vor allem bei `ESLint` relevant, da UI5-Projekte eine andere Konfiguration wie CAP/Node.js Projekte benötigen.

### ESLint Konfiguration

Die Konfiguration erfolgt mit der Datei `.eslintrc.json`.

```json
{
    "env": {
        "browser": true,
        "es2021": true
    },
    "globals": {
        "$": true,
        "sap": true,
        "jQuery": true
    },
    "extends": [
        "airbnb-base",
        "prettier"
    ],
    "parserOptions": {
        "ecmaVersion": 12
    },
    "rules": {
        "linebreak-style": "off",
        "no-underscore-dangle": ["error", { "allowAfterThis": true }],
        "prefer-rest-params": "off",
        "arrow-body-style": "off",
        "prefer-arrow-callback": "off",
        "spaced-comment": "off",
        "func-names": "off",
        "no-restricted-syntax": "off"
    },
    "ignorePatterns": [ 
        "test/*", 
        "dist/*",
        "localService/*"
    ] 
}
```

> Die Integration von `Prettier` in `ESLint` sorgt dafür, dass sämtliche Regeln im Zusammenhang mit der Formatierung deaktiviert werden.

### Prettier Konfiguration

Die Konfiguration erfolgt mit der Datei `.prettierrc.json`. Mit Ausnahme der untenstehenden Regel werden die [Standardregeln](https://prettier.io/docs/en/options.html) angewendet.

```json
{
  "singleQuote": true
}
```

Die Formatierung kann mit Hilfe der Datei `.prettierignore` für Dateien und Verzeichnisse deaktiviert werden. In der Regel sollten generierte Artifakte nicht automatisch formatiert werden, wobei solche normalerweise auch nicht über ein Repository verwaltet werden.

```text
dist
```


## Verwendung

Während `ESLint` den Code laufend überprüft und Probleme visuell darstellt, wird `Prettier` normalerweise manuell ausgeführt. Die verschiedenen IDEs unterstützen diese beiden Tools entweder direkt oder mit Hilfe von entsprechenden Extensions, die manuell installiert werden müssen.

`ESLint` ist in der Lage verschiedene Probleme automatisch zu korrigieren - entweder einzeln oder alle Vorkommnisse einer Datei. Zudem können mit ESLint auch Regeln deaktiviert werden. Hierzu stehen die folgenden vordefinierten Kommentare zu Verfügung.

```javascript
/* eslint-disable <regel> */
// eslint-disable-next-line <regel>
```

> Es ist **nicht** erlaubt Regeln für gesamte Dateien zu deaktivieren. Das vereinzelte Deaktivieren von Regeln ist in absoluten Ausnahmefällen gestattet, sollte aber nicht aus Bequemlichkeit erfolgen!

Für Prettier kann die automatische Formatierung ebenfalls für einzelne Zeile deaktiviert werden.

```javascript
// prettier-ignore
```

> Eine einheitliche Formatierung ist sehr wichtig, damit ein korrekter und einfacher Vergleich von zwei Code-Versionen möglich ist. Aus diesem Grund wird über zusätzliche Werkzeuge sichergestellt, dass jede geänderte Datei [vor dem Commit automatisch formatiert](ui5/gitintegration) wird.