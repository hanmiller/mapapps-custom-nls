# Custom nls
This bundle allows to customize the default nls strings that are used in map.apps (e.g. for tool titles or other ui elements).

If you want to change the title of a ui element in map.apps, you can simply do this by adding nls files to your app. But if you want to apply text changes to multiple apps, using a custom nls bundle is a better solution. Adding or changing strings in the future can be done in that bundle and once you have uploaded the new version of this bundle, all apps use the new text strings immediately.

### Sample App ###
http://www.mapapps.de/mapapps/resources/apps/downloads_customnls/index.html

In this sample app, the title of the Map Flow tool in the lower left corner is changed from "Map Content"/"Karteninhalt" to "Topics"/"Themen".

Usage Guide
------------------
To add your own nls customizations, at first download the bundle and extract the zip file. In the zip file you will find two bundle.js files in the folder "nls" (for English) and in "nls/de" (for German).

Open this files in a text editor and add the nls strings that you want to customize. Sample:
```
define({
    root:
    ({
        "basemaptoggler": {
            "ui": {
                "labelTitle": "Background"
            }
        },
        "mapflow": {
            "tool": {
                "title": "Topics"
            }
        }
    }),
    "de": true
});
```

A full list of all available nls string can be found here: <TBD>

After saving your changes, zip all contents of the bundle folder and upload the zip file via the map.apps Manager bundle management tab.

Now add the bundle to all of your apps, that should use the customized nls strings.

Adding a completely new language to map.apps
------------------
If you want to add a completely new language to your map.apps installation, please have a look at this tool: http://developernetwork.conterra.de/en/downloads/tools/how-generate-additional-language-bundles-mapapps
