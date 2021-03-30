# Coding Guidelines

Mit Hilfe von Coding Guidelines kann die Code Qualität erhöht werden. Gleichzeitig vereinfacht einheitliches Coding die Wartung und verkürzt das Onboarding von neuen Entwicklern. Allerdings nützen umfangreiche Regelwerke nicht, wenn diese nicht kontrolliert und eingehalten werden. In diesem Sinne scheint es logisch, dass einerseits die Anzahl Regeln in Grenzen gehalten und der Code auch überprüft wird.

Für diesen Zweck bieten sich insbesondere zwei Tools besonders gut an. Mit `ESLint` können statische Code Analysen durchgeführt und problematische Muster erkannt werden. `Prettier` hilft, dass Code einheitlich formattiert wird, was insbesondere bei der Verwendung von `Git` für wesentlich bessere und transparentere Ergebnisse sorgt.

Da sich der Funktionsumfang von `ESLint` und `Prettier` teilweise überschneiden, muss das Zusammenspiel konfiguriert werden.

## Prettier

`Prettier` ist ein Code Formatter, der verschiedene Sprachen unterstützt. Prettier wendet dabei verschiedene Regeln an, die unter Umständen die eigenen Gewohnheiten überschreiben, da der Code immer gesamtheitlich nach den konfigurierten Regeln formatiert wird. 


### Installation

```bash
npm install prettier --save-dev --save-exact
```

> Der Parameter --save-exact ist **zwingend** zu verwenden, da Prettier auch in Minor-Versionen die Formattierung verändern kann.

Die für `ESLint` nicht mehr relevanten Regeln können durch die Installation des entsprechenden `Prettier`-Plugins deaktiviert werden.

```bash
npm install eslint-config-prettier --save-dev
```

### Konfiguration

Die Konfiguration erfolgt in der Datei `.prettierrc`. Aktuell wird keine Konfigurationdatei benötigt, da die Standardkonfiguration den Anforderungen genügt.

### Automatische Formattierung



## ESLint

ESLint ist ein statisches Code-Analyse-Tool zum Identifizieren problematischer Muster im JavaScript Code. Gleichzeitig kann damit auch sichergestellt werden, dass bestimmte Guidelines und Best-Practices eingehalten werden.

### Installation

```bash
npm install eslint --save-dev
```

Für die Verwendung in UI5 Projekten stehen weitere Pakete zu Verfügung, die installiert werden müssen.

```bash
npm install eslint-plugin-ui5 --save-dev
```
```bash
npm install eslint-config-ui5 --save-dev
```

### Konfiguration

Die Konfiguration erfolgt in der Datei `.eslintrc`. Diese Datei kann im Projekt mehrfach vorhanden sein, damit unterschiedliche Konfigurationen (z.B. für das UI und Backend) möglich sind. Die Datei wird dabei ausgehend von der jeweiligen Datei in der Ordnerhierachie gesucht.

```json
{
    "env": {
        "browser": true,
        "es2021": true
    },
    "globals": {
        "$": true
    },
    "extends": [
        "ui5",
        "prettier"
    ],
    "parserOptions": {
        "ecmaVersion": 12
    },
    "rules": {
        "linebreak-style": "off"
    },
    "ignorePatterns": [ 
        "test/*", 
        "dist/*"
    ] 
}
```
