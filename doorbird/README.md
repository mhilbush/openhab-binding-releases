Download the above jar file and place it in the addons directory.

See README here. This will be updated as I work on improving the documentation (it's a little sparse at the moment).

https://github.com/mhilbush/openhab2-addons/tree/doorbird-binding-bnd/bundles/org.openhab.binding.doorbird

The binding depends on the JNA feature, so you may need to install that feature from the Karaf console.
```
feature:install openhab-runtime-jna
```

There are still features missing from the binding:

- channel for video stream (or URL of video stream)
- others???
