# ESLint

[`ESLint`](https://eslint.org/) ist ein sehr flexibles, statisches Code-Analyse Tool für JavaScript, mit dem problematische Anweisungen gefunden und teilweise auch automatisch behoben werden können. 

Innerhalb eines Projektes können unterschiedliche Konfiguration angelegt werden, die jeweils in der Ordnerhierachie nach unten vererbt werden. Damit ist es möglich in Multi-Target Anwendungen verschiedene Konfigurationen für unterschiedliche Zielumgebungen (z.B. Node.js Server, Browser) anzulegen.

## Installation

```bash
npm install eslint --save-dev
```

## Konfiguration 

Die Konfiguration erfolgt in einer oder mehreren Konfigurationsdateien mit dem Namen `.eslintrc`.

- Konfiguration von [UI5 Anwendungen](ui5/eslint.md)
- Konfiguration von CAP Anwednungen

## Verwendung

`ESLint` wird normalerweise laufend ausgeführt und Meldungen laufend in der IDE visualisiert. Nebst der Prüfung von Code kann `ESLint` auch verschiedene Probleme einzeln oder für ganze Dateien korrigieren. 

In Ausnahmefällen kann es sinnvoll oder notwendig sein, dass Regeln deaktiviert werden müssen. Die Deaktivierung erfolgt über den nachfolgenden Kommentar unmittelbar vor der betroffenen Zeile.

```javascript
// eslint-disable-next-line <regel>
```

Es ist grundsätzlich auch möglich, Regeln für gesamte Dateien zu deaktivieren, dies ist jedoch explizit **nicht** erlaubt.