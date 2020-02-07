See full README at the following link.

https://github.com/mhilbush/openhab2-addons/tree/doorbird-a1081/bundles/org.openhab.binding.doorbird

Download these dependencies and place in your addons directory **before** you download the doorbird jar file.
- jna-5.5.0.jar
- resource-loader-1.3.7.jar
- lazysodium-java-4.2.5.jar

The *jna* jar might not be needed as it might be installed by another binding.
You can check if it's already installed by running **list -s | grep jna** in the Karaf console.

Once you've downloaded and installed the dependencies, download the *org.openhab.binding.doorbird-2.5.2-SNAPSHOT.jar* jar file and place it in the addons directory.

If you're already running an old version of the binding, after you install a new version you may need to delete and readd the thing in order to pick up the latest channel definitions.

If you have any feedback on bugs and/or features, please post on this community thread.

https://community.openhab.org/t/doorbird-binding/73564
