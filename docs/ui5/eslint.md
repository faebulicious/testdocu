# ESLint

ESLint ist ein statisches Code-Analyse-Tool zum Identifizieren problematischer Muster im JavaScript Code. Gleichzeitig kann damit auch sichergestellt werden, dass bestimmte Guidelines und Best-Practices eingehalten werden.

Die Installation erfolgt via <code>npm</code>. Die Installation sollte im Projekt mit Entwicklungsabhängigkeit erfolgen.

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

Für ESLint wird eine Konfigurationsdatei benötigt. Die Konfigurationsdatei wird dabei entlang der Hierarchie gesucht. Entsprechend ist es möglich innerhalb eines Projekte mehrere Konfigurationen anzulegen (z.B. für UI5 und Cap Artifakte).

Die nachfolgende Konfigurationsdatei 

```json
module.exports = {
    "env": {
        "browser": true,
        "commonjs": true,
        "es2021": true
    },
    "globals": {
        "$": true
    },
    "extends": "ui5",
    "parserOptions": {
        "ecmaVersion": 12
    },
    "rules": {
        "linebreak-style": "off",
        "one-var": "off",
        "quotes": "off",
        "no-console": "off",
        "default-case": "off",
        "no-multi-spaces": "off",
        "ui5/hungarian-notation": "off",
        "ui5/no-global-name": "off",
        "sap-no-history-manipulation": "off",
        "no-nested-ternary": "off",
        "camelcase": "off",
        "key-spacing": "off",
        "no-lonely-if": "off",
        "no-continue": "off",
        "no-else-return": "off"
    }
};
```
