See the README [here](https://github.com/mhilbush/openhab2-addons/blob/weather-company-binding/addons/binding/org.openhab.binding.weathercompany/README.md).

Remember, when you install a new version, you may need to delete and readd 
the Weather thing in order to pick up new or changed channels.

Also, if you're on an older version of openHAB, you may need to drop this jar file into your addons directory in order to avoid this missing dependency error.

http://central.maven.org/maven2/com/google/code/gson/gson/2.8.2/gson-2.8.2.jar

```
2019-05-04 07:04:58.111 [WARN ] [org.apache.felix.fileinstall        ] - Error while starting bundle: file:/opt/openhab2/addons/org.openhab.binding.weathercompany-2.5.0-SNAPSHOT.jar
org.osgi.framework.BundleException: Could not resolve module: org.openhab.binding.weathercompany [274]
  Unresolved requirement: Import-Package: com.google.gson; version="[2.8.0,3.0.0)"
```
