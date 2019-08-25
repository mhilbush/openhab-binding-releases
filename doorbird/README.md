See full README at the following link.

https://github.com/mhilbush/openhab2-addons/tree/doorbird-new/bundles/org.openhab.binding.doorbird

This binding depends on some 3rd party libraries that are not part of the openHAB distribution.
Download these dependencies and place in your addons directory **before** you download the doorbird jar file.
- com.goterl.lazycode.lazysodium-java-4.0.1.jar
- jna-5.3.0.jar

The jna-5.3.0.jar might not be needed as it might be installed by another binding.
You can check if it's already installed by running **list -s | grep jna** in the Karaf console.

Once you've downloaded and installed the dependencies, download the *org.openhab.binding.doorbird-2.5.0-SNAPSHOT.jar* jar file and place it in the addons directory.

If you're already running the bining, after you install a new version you may need to delete and readd the thing in order to pick up the latest channel definitions.

There are still some features missing from the binding:

- channel for video stream (or URL of video stream)
- channel for RFID
- others???

If you have any feedback on bugs and/or features, please post on this community thread.

https://community.openhab.org/t/doorbird-binding/73564
