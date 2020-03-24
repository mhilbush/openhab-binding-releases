# Squeezebox dev/test releases

## How To Install

- Download the jar file from this repo (click on the jar file, then press the **Download** button)

- Uninstall any other version of the squeezebox binding that was installed through PaperUI or `conf/services/addons.cfg`

- Install the upnp feature using the following Karaf console command. Note: Bindings installed in the addons directory don't have their dependencies automatically installed. The SqueezeBox binding depends on upnp, which might've been uninstalled when you uninstalled the binding.

```
feature:install openhab-transport-upnp
```

- Place the new squeezebox binding into the `openhab2/addons` directory


If you need to see what's going on, enable debugging

- Turn on DEBUG level logging using this command

```
log:set DEBUG org.openhab.binding.squeezebox
```

- Turn off DEBUG level logging using this command

```
log:set INFO org.openhab.binding.squeezebox
```
