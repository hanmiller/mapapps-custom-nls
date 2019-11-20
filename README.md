# mapapps-custom-nls

This project demonstrates how to build a custom language bundle.

* [Requirements](https://github.com/conterra/mapapps-4-developers#requirements)
* [Usage](https://github.com/conterra/mapapps-4-developers#usage)
* [Updating from older versions](https://github.com/conterra/mapapps-4-developers#updating-from-older-versions)
* [References](https://github.com/conterra/mapapps-4-developers#references)

## Requirements

* map.apps 4.7.2
* all resources from `map.apps-VERSION/sdk/m2-repository` need to be copied manually to your local Maven repository (e.g. `%UserProfile%/.m2/repository` for Windows, `~/.m2/repository` for MacOS).

Prepare `application.properties` for the additionl language
```properties
client.config.supportedLocales=en,de,<your language code>
```

## Preparation
* Rename folder `mapapps-custom-nls\src\main\js\bundles\language-pack\nls\en` with your country code, e.g. `mapapps-custom-nls\src\main\js\bundles\language-pack\nls\fr`
* Edit file `mapapps-custom-nls\src\main\js\bundles\language-pack\nls\bundle.js` and replace `en` with your country code
``` 
module.exports = {
    root: {},
    "fr": true
};
```
* Add your translations to file `mapapps-custom-nls\src\main\js\bundles\language-pack\nls\fr\bundle.js`

## Usage

The project supports a 'remote project' and 'standalone project' mode.

### Use 'remote project' mode

In this mode a map.apps installation is available elsewhere and most JavaScript resources are fetched from this installation.
This mode is recommended.

The URL of the map.apps server can be declared in the pom.xml. 

Replace

```xml
 <mapapps.remote.base>.</mapapps.remote.base>
```

with

```xml
 <mapapps.remote.base>http://yourserver/mapapps</mapapps.remote.base>
```

As an alternative the URL can be declared in a file called `build.properties` with the content

```properties
mapapps.remote.base=http://yourserver/mapapps
```

and enabling the "env-dev" Maven profile.
Append `-P env-dev` or `-Denv=dev` to any Maven execution or declare the profile as activated by default in your Maven settings.xml.

### Use 'standalone project' mode

In this mode all JavaScript sources are added to this project during development.
The drawback of this mode is that you can not test authentication and that the default settings are not read from the remote instance.

This mode requires that the profile `include-mapapps-deps` is activated.
Append `-P include-mapapps-deps` to any Maven execution or declare the profile as activated by default in your Maven settings.xml.

### Start a local HTTP server

Start the integrated Jetty server with:

```sh
mvn clean jetty:run -P watch-all
```

Make sure that the `watch-all` Maven profile is activated.
The profile will start a gulp task that watches for changes in your source code.

After a successfull start the Jetty server ist available at [http://localhost:9090](http://localhost:9090).

### Skip intallation of Node.js and npm during Maven execution

By appending `-Denv=dev -Dlocal.configfile=./build.properties` to any Maven execution the development mode is activated.
This means:

* Node.js and npm are not installed
* watch-all profile is activated
* the build.properties file is loaded

To enforce the installation of Node.js and npm execute:

```
mvn initialize
```

This triggers the installation of Node.js and npm exclusively.

### Make your code bundle ready

To ensure that all files are compressed/minified and a dependencies.json is calculated execute:

```sh
mvn clean install -P compress
```

### Upload your code to a map.apps installation

To upload your apps and bundles after compression append the `upload` profile.

```sh
mvn clean install -P compress,upload
```