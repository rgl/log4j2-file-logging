# About

This is a log4j2 file logging example.

# Usage

Install the dependencies:

* [Visual Studio Code](https://code.visualstudio.com).
* [Dev Container plugin](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).

Open this directory with the Dev Container plugin.

Open the Visual Studio Code Terminal.

Build:

```bash
gradle dependencies
gradle build --warning-mode all
jar tf build/libs/example-1.0.0.jar
```

Execute:

```bash
rm -rf logs
gradle run
ll logs
# then execute gradle run several times, to see how it rotates the files.
# as configured, no more than 3 files per day will exist.
gradle run
ll logs
```
