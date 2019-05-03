See README at the following link. I will update that README as I add features and improve the documentation (it's a little sparse at the moment).

https://github.com/mhilbush/openhab2-addons/tree/doorbird-new/bundles/org.openhab.binding.doorbird

This binding depends on some 3rd party libraries that are not part of the openHAB distribution.
These libraries are contained in the *doorbird-deps-1.0.0.jar* file located in this repository.
Download this jar file and place it in your addons directory **before** downloading and installing the *org.openhab.binding.doorbird-2.5.0-SNAPSHOT.jar*.

**NOTE:** The binding depends on a encryption library called libsodium. 
I don't know if this library will work on a pi. 
If you're running a pi and can confirm if it works or not, please post your experience using the above link.

Once you've downloaded and installed the dependencies jar, download the *org.openhab.binding.doorbird-2.5.0-SNAPSHOT.jar* jar file and place it in the addons directory.

If you're already running the bining, after you install a new version you may need to delete and readd the thing in order to pick up the latest channel definitions.

There are still some features missing from the binding:

- channel for video stream (or URL of video stream)
- channel for RFID
- others???

If you have any feedback on bugs and/or features, please post on this community thread.

https://community.openhab.org/t/doorbird-binding/73564
