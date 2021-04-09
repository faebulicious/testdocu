# Transkompilierung mit Babel

[`Babel`](https://babeljs.io/) ist ein JavaScript Transcompiler. Babel wandelt moderne ECMAScript 2015+ Syntax in rückwärtskompatible Syntax um, damit der Code auch in älteren Umgebungen einwandfrei funktioniert. Der Vorteil von `Babel` liegt darin, dass sich Entwickler nicht mehr um die Kompatibilität kümmern müssen und die neusten Features nutzen können. Babel ist entsprechend für im Browser laufenden Anwendungen elementar, da die Zielumgebung nicht klar ist und beeinflusst werden kann.

## Installation

```bash
npm install @babel/core @babel/cli @babel/preset-env @babel/node @babel/runtime --save-dev
```

## Konfiguration

Die Konfiguration erfolgt in einer Konfigurationsdateien mit dem Namen `.babelrc`.

```json
{
    "presets": [
        "airbnb"
    ]
}
```