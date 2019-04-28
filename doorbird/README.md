See README here. This will be updated as I work on improving the documentation (it's a little sparse at the moment).

https://github.com/mhilbush/openhab2-addons/tree/doorbird-new/bundles/org.openhab.binding.doorbird

This binding depends on some 3rd party libraries that are not part of the openHAB distribution.
These libraries are contained in the *doorbird-deps-1.0.0.jar* file located in this repository.
Download this jar file and place it in your addons directory **before** downloading and installing the *org.openhab.binding.doorbird-2.5.0-SNAPSHOT.jar*.

Once you've downloaded and installed the dependencies jar, download the *org.openhab.binding.doorbird-2.5.0-SNAPSHOT.jar* jar file and place it in the addons directory.

You may need to delete and readd the thing in order to pick up the latest channel definitions.

There are still some features missing from the binding:

- channel for video stream (or URL of video stream)
- channel(s) for doorbell and motion history
- others???
