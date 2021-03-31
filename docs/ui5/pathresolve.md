# Pfadauflösung

Werden aus einer UI5 App Ressourcen (z.B. Bilder, Service, APIs) angesprochen dann muss dies entweder über URIs, absolute oder relative Pfade geschehen.

Der Zugriff über URIs ist grundsätzlich in vielen Fällen nicht ideal, da diese nicht statisch bekannt sind und sich auch ändern können. Absolute Pfade sind ebenso ungeeignet, weil dies impliziert, dass die Struktur der Subpfade ebenfalls statisch sein muss. Es bleiben folglich nur noch relative Pfade, die allerdings nicht in jedem Fall funktionieren, da das realtive Wurzelverzeichnis nicht zwingend das Wurzelverzeichnis der UI5 App sein muss (z.B. bei der Integration im Portal).

SAP stellt deswegen für relative Pfade an einigen Stellen implizite Logik bereit:
- In der `manifest.json` definierte Pfade von Datenquellen (`dataSources`) werden zur Laufzeit automatich in vollständige und korrekte URIs aufgelöst
- Die lokale Testumgebung von CAP Anwendungen behandelt auch relative Pfade korrekt und leitet die Anfragen intern an die Services um
- Der Task `webide-extension-task-updateManifestJson` wandelt beim Build absolute Pfade in der `manifest.json` in relative um

> Sämtliche Pfade müssen deshalb grundsätzlich **relativ** definiert werden, also ohne führenden Slash /

Problematisch wird es jedoch, wenn Ressourcen in Javascript angesprochen wird (z.B. Bilder, AJAX Calls, usw.). Dort werden relative Pfade nicht out-of-the-box in korrekte URIs umgewandelt.

Als einzige Lösung bleibt die dynamische Erzeugung der Ziel-Pfade (wie es auch für die UI5 Datenquellen initial passiert). Der Code dafür impliziert keine eigenen Logik sondern verwendet die von SAP bereitgestellte Logik und kann einfach in einem Basis Controller bereitgestellt werden.

```javascript
sap.ui.define(
  [
    'sap/ui/core/mvc/Controller',
  ],
  function (Controller) {
    return Controller.extend('foo.bar', { // Namespace
      resolveUri(sPath) {
        return this.getOwnerComponent().getManifestObject().resolveUri(sPath);
      },
    });
  },
);
```