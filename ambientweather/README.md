# Ambient Weather Dev/test Releases

See full README [here](https://github.com/mhilbush/openhab2-addons/blob/ambient-weather-binding/bundles/org.openhab.binding.ambientweather/README.md).

If you run into issues, please post on the community thread here.
https://community.openhab.org/t/ambient-weather-weather-station-binding/59315

## How To Install

Put these two files in your addons directory.
- ambient-weather-deps-1.0.0.jar
- org.openhab.binding.ambientweather-2.5.0-SNAPSHOT.jar

Here are the steps you need to follow to install the binding.

Go to the My Account page of your ambientweather.net dashboard and request an application key and an API key. You’ll need both of these keys to use the binding. You can get the API key immediately by clicking on the Create API Key button. For the application key, you need to email ambient weather using the support email address that’s at the bottom of the My Account page. They’ll want the MAC address of your station and the email address you used to create your dashboard account. Tell them in the email that you’re testing the openHAB binding. It may take a day or so to get the Application key.

You’ll need the API and Application keys before you can continue with the remaining steps.

In Paper UI, add an Ambient Weather Bridge thing. This is where you need to enter the Application and API keys.

In Paper UI, add the Ambient Weather station that matches the model of your station. If your model is not listed, try the WS-1400-IP. Select the bridge, and enter the MAC address of your station. If you want your model added as a thing type, PM me and we'll try to get it sorted out.

After a minute or two you should start seeing the sitemap data get updated. If you don’t see anything update, ping me and I’ll help you get it sorted out.
