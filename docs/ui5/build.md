# Build

Durch das Builden einer App wird diese für den produktiven Einsatz vorbereitet und optimiert. Voraussetzung für das Builden von Apps sind die `UI5 Tools` und entsprechenden Konfigurationsdateien.

```bash
npm install @ui5/cli --save-dev
```

## Standalone 

Standalone Apps werden normalerweise mit Hilfe des `Yeoman`-Generators oder anhand einer Vorlage angelegt. Die notwendingen Abhängigkeiten sind bereits in der `package.json` beschrieben und die notwendige Konfiguration ist bereits in der Datei `ui5.yaml` abgelegt.

## MTA

Wird eine App als Teil einer Multitarget-App (MTA) deployed, wird ein abweichender Build Prozess benötigt, da die vorbereiteten Artifakte in einem Zip-Archiv abgelegt und in das HTML5 Repository hochgeladen werden muss.

Für den Build Prozess werden weitere `npm` Packete benötigt.

```bash
npm install ui5-task-zipper --save-dev
```
```bash
npm install @sap/ui5-builder-webide-extension --save-dev
```

> Durch die Installation werden die Pakete zwar als `devDependencies` registiert, für den Build Prozess ist es jedoch notwendig, dass diese in der `package.json` auch als ui5 Dependency registriert werden.

```json
{
  "name": "sales_catalog",
  "version": "0.0.1",
  "devDependencies": {
    ...
    "@sap/ui5-builder-webide-extension": "1.0.x",
    "ui5-task-zipper": "^0.3.1"
  },
  ...
  "ui5": {
    "dependencies": [
      "@sap/ui5-builder-webide-extension",
      "ui5-task-zipper",
    ]
  },
}
```

Beide Packete stellen weitere Aufgaben für den UI5 Builder bereit. Für den eigentlichen Build wird nun eine Konfigurationsdatei `ui5-deploy-mta.yaml` benötigt. Der Dateiname folgt nicht einem vordefinierten Muster, sondern dient der Unterscheidung von weiteren Konfiguration und wird für den Build Prozess verwendet.

```yaml
specVersion: '1.0'
metadata:
  name: <app> ## Name of Application
type: application
resources:
  configuration:
    propertiesFileSourceEncoding: UTF-8
builder:
  resources:
    excludes:
      - "/test/**"
      - "/localService/**"
  customTasks:
  - name: webide-extension-task-updateManifestJson
    afterTask: generateVersionInfo
    configuration:
      appFolder: webapp
      destDir: dist
  - name: ui5-task-zipper
    afterTask: generateCachebusterInfo
    configuration:
      archiveName: <archive> #Name of Archive File (reuise in mta.yaml) without Extension!
      additionalFiles:
      - xs-app.json
```

Der Task `webide-extension-task-updateManifestJson` aktualsiert die `manifest.json`. Unter anderem werden automatisch führende Slashes in den Pfaden von Datenquellen entfernt. Der Task `ui5-task-zipper` verpacket den Inhalt des `dist` Verzeichnis in ein Zip-Archiv. Zudem können weitere Dateien deklariert werden, die ebenfalls hinzugefügt werden sollen, in diesem Fall die lokale App Router Definition `xs-app.json`.

Für das Ausführen der Build Prozesses eignet sich am besten ein NPM Script, das in der Datei `package.json` definiert wird.

```json
{
  ...
  "scripts": {
    ...
    "build:mta": "ui5 build preload --clean-dest --config ui5-deploy-mta.yaml --include-task=generateManifestBundle generateCachebusterInfo",
  }
}
```

> Dieses Script muss vom Build Prozess der MTA aufgerufen werden. Ebenso muss sichergestellt sein, dass der Name der Zip-Archiv übereinstimmt.

## MTA Update

Ist eine Anwendung erstmalig mittels MTA deployed, bietet es sich an weitere Änderungen direkt in das HTML5 Repository zu pushen. Die Voraussetzung sind hierbei gleich wie für das Builden für die MTA, allerdings sieht der Build Prozess etwas anders aus, da keine Zip-Datei mehr benötigt wird, sondern direkt das `dist` Verzeichnis gepushed werden kann.

Für den Build Prozess wird eine separater Konfigurationsdatei `ui5-deploy.yaml` benötigt.

```yaml
specVersion: '1.0'
metadata:
  name: <app> ## Name of Application
type: application
resources:
  configuration:
    propertiesFileSourceEncoding: UTF-8
builder:
  resources:
    excludes:
      - "/test/**"
      - "/localService/**"
  customTasks:
  - name: webide-extension-task-updateManifestJson
    afterTask: generateVersionInfo
    configuration:
      appFolder: webapp
      destDir: dist
  - name: webide-extension-task-resources ## required?
    afterTask: webide-extension-task-updateManifestJson
    configuration:
      nameSpace: com.bmc
  - name: webide-extension-task-copyFile
    afterTask: webide-extension-task-resources
    configuration:
      srcFile: "/xs-app.json"
      destFile: "/xs-app.json"
```

Für das Ausführen des Build Prozesses wird ein weitere NPM Script in der `package.json` definiert.

```json
{
  ...
  "scripts": {
    ...
    "build:cf": "ui5 build preload --clean-dest --config ui5-deploy.yaml     --include-task=generateManifestBundle generateCachebusterInfo"",
  }
}
```

Anschliessend kann das `dist` Verzeichnis ganz einfach ins HTML5 Repository gepushed werden.

```bash
cf html5-push -r ./dist
```