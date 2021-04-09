# Code Analyse mit ESLint

## Voraussetzungen

- **ESLint** ist im Projekt [installiert](tools/eslint.md#installation). 
- **Prettier** ist im Projekt [installiert und konfiguriert](tools/prettier.md).

## Installation

Zusätzlich wird für `ESLint` die AirBnb Basiskonfiguration benötigt, welche die Grundkonfiguration von `ESLint` vornimmt und auch für die Verwendung von `Babel` vorbereitet ist.

```bash
npm install eslint-config-airbnb-base --save-dev
npx install-peerdeps --dev eslint-config-airbnb-base
```

## Konfiguration 

> Die Konfiguration von `ESLint` hängt primär von der Zielumgebung ab. Diese ist jedoch gerade auf Client-Seite oftmals nicht eindeutig bekannt da Benutzer unterschiedliche Browser und Versionen einsetzen.
>
> Dieser Umstand schliesst eine spezifische Konfiguration für eine bestimmte Umgebung aus. Gleichzeitig würde die Verwendung einer möglichst Rückwärtskompatiblen Konfiguration dazu führen, dass moderne Features der Sprache nicht verwendet werden könnten.
>
> **Aus diesem Grund soll auch für Browser-Umgebungen die jeweils modernste Syntax verwendet und anschliessend mit [Babel transkompiliert](tools/babel.md) werden.** Dabei wird moderne Syntax in kompatible Syntax umgewandelt.

Die Konfiguration von `ESLint` erfolgt in der Datei `.eslintrc`. Bei mehreren UI5 Anwendung kann diese Datei auch einmalig im Stammverzeichnis sämtlicher Anwendungen angelegt werden.

```json
{
    "env": {
        "browser": true,
        "es2020": true,
        "jquery": true
    },
    "globals": {
        "sap": true
    },
    "extends": [
        "airbnb-base",
        "prettier"
    ],
    "rules": {
        "no-underscore-dangle": [0, { "allowAfterThis": true }],
        "prefer-arrow-callback": 1,
        "func-names": 0,
        "object-shorthand": [0, "consistent"],
        "no-console": 0
    },
    "ignorePatterns": [ 
        "test/*", 
        "dist/*",
        "localService/*",
        "approuter/*",
        "deployer/*",
        "mta_archives/*",
        "karma*.js"
    ] 
}
```

> Die `ignorePatterns` können je nach Anwendung abweichen.

## Regeln

Verschiedene Regeln des AirBnb Regelsets werden explizit überschrieben:

| Regel | Beschreibung |
| ----- | ------------ |
| [no-underscore-dangle](https://eslint.org/docs/rules/no-underscore-dangle#disallow-dangling-underscores-in-identifiers-no-underscore-dangle) | Angepasst an SAP Standard |
| [prefer-arrow-callback](https://eslint.org/docs/rules/prefer-arrow-callback#require-using-arrow-functions-for-callbacks-prefer-arrow-callback) | Angepasst an SAP Standard |
| [func-names](https://eslint.org/docs/rules/func-names#require-or-disallow-named-function-expressions-func-names) | Angepasst an SAP Standard |
| [object-shorthand](https://eslint.org/docs/rules/object-shorthand#require-object-literal-shorthand-syntax-object-shorthand) | Angepasst an SAP Standard |
| [no-console](https://eslint.org/docs/rules/no-console#disallow-the-use-of-console-no-console) | Wird zugelassen, da durch Transkompilierung entfernt |


