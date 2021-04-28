# Code Formattierung mit Prettier

## Voraussetzungen

- **Prettier** ist im Projekt [installiert und konfiguriert](tools/prettier.md).

## Installation

Werden in UI5 XML Views verwendet, können diese ebenfalls mit Prettier formatiert werden. Hierzu muss ein zusätzliches Plugin installiert werden.

```bash
npm install @prettier/plugin-xml --save-dev
```

## Konfiguration

Es ist keine zusätzliche Konfiguration notendig.

## Verwendung

`Prettier` wird in der Regel manuell, spätestens jedoch beim [Commit](git/prettier.md) ausgeführt.

Um zu verhindern, dass bestimmte XML-Zeilen formatiert werden, kann folgender Kommentar vor die entsprechende Zeile gestellt werden.

```xml
<foo>
  <!-- prettier-ignore-start -->
    <this-content-will-not-be-formatted    />
  <!-- prettier-ignore-end -->
</foo>
```