# Squeezebox dev/test releases

## How To Install

- Download the jar file from this repo (click on the jar file, the press the **Download** button)

- Uninstall any other version of the squeezebox binding that was installed through PaperUI or `conf/services/addons.cfg`

- Install the upnp feature using this console command

```
feature:install openhab-transport-upnp
```

- Place the new squeezebox binding into the `openhab2/addons` directory

- Turn on DEBUG level logging using this command

```
log:set DEBUG org.openhab.binding.squeezebox
```
