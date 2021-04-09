# ESLint

## Voraussetzungen

> Beim Initialisieren von CAP Projekten wird zwar bereits eine `ESLint` Konfiguration angelegt, die notwendingen Werkzeuge werden jedoch **nicht** automatisch installiert.

- **ESLint** ist im Projekt [installiert](tools/eslint.md#installation). 
- **Prettier** ist im Projekt [installiert](tools/prettier.md#installation) und [konfiguriert](ui5/prettier.md#konfiguration).

## Konfiguration 

Die durch die Initialisierung erzeugte Konfigurationsdatei `.eslintrc` kann grundsätzlich übernommen werden, **muss** aber erweitert werden, damit `Prettier` korrekt integriert wird.

```json
{
    "extends": [
        "eslint:recommended",
        "prettier" // <-- Erweiterung für Prettier muss hinzugefügt werden
    ],
    "env": {
        "node": true,
        "es6": true,
        "jest": true
    },
    "parserOptions": {
        "ecmaVersion": 2017
    },
    "globals": {
        "SELECT": true,
        "INSERT": true,
        "UPDATE": true,
        "DELETE": true,
        "CREATE": true,
        "DROP": true,
        "cds": true
    },
    "rules": {
        "no-console": "off",
        "require-atomic-updates": "off"
    }
}
```