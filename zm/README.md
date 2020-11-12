# Zoneminder Binding

Supports the Zoneminder video surveillance system.

## Supported Things

The following thing types are supported:

| Thing    | ID       | Discovery | Description |
|----------|----------|-----------|-------------|
| Server   | server   | Manual    | Server bridge manages all communication with Zoneminder server |
| Monitor  | monitor  | Automatic | Monitor represents a Zoneminder camera monitor |

## Installation

The binding requires Zoneminder version 1.34.0 or greater and API version 2.0 or greater.
It also requires that you enable the **OPT_USE_API** parameter in the Zoneminder configuration.

If your Zoneminder is installed using a non-standard URL path or port number, that must be specified when you add the Zoneminder server thing.

There are two different styles of operation, depending on whether or not you have Zoneminder configured to use authentication.

### Non-Authenticated

If Zoneminder authentication is not used, the User and Password parameters should be empty in the *Zoneminder Server* thing configuration.
No other configuration is required.

### Authenticated

If Zoneminder authentication is used, first make sure the Zoneminder user has the **API Enabled** permission set in the Zoneminder Users configuration.
Then, enter the user name and password into the Zoneminder Server thing configuration.

## Discovery

The server bridge must be added manually.
Once the server bridge is configured with a valid Zoneminder host name or IP address, 
all monitors associated with the Zoneminder server will be discovered.

## Thing Configuration

### Server Thing

The following configuration parameters are available on the Server thing:

| Parameter | Parameter ID | Required/Optional | Description |
|-----------|--------------|-------------------|-------------|
| Host                           | host                        | Required  | Host name or IP address of the Zoneminder server. |
| Use secure connection          | useSSL                      | Required  | Use http or https for connection to Zoneminder. Default is http. |
| Port Number                    | portNumber                  | Optional  | Port number if not on Zoneminder default port 80. |
| Use Default Url Path           | useDefaultUrlPath           | Required  | If ON, use Zoneminder default of /zm; if OFF, use value from urlPath parameter. |
| Url Path                       | urlPath                     | Optional  | Use this parameter when not using the Zoneminder default path of /zm. |
| Refresh Interval               | refreshInterval             | Required  | Frequency at which monitor status will be updated. |
| Default Alarm Duration         | defaultAlarmDuration        | Required  | Can be used to set the default alarm duration on discovered monitors. |
| Default Image Refresh Interval | defaultImageRefreshInterval | Optional  | Can be used to set the image refresh interval on discovered monitors. Leave empty to not set an image refresh interval. |
| Monitor Discovery Enabled      | discoveryEnabled            | Required  | Enable/disable the automatic discovery of monitors. Default is enabled. |
| Monitor Discovery Interval     | discoveryInterval           | Required  | Frequency at which the binding will try to discover monitors. |
| User ID                        | user                        | Optional  | User ID of Zoneminder user when using authentication. |
| Password                       | pass                        | Optional  | Password of Zoneminder user when using authentication. |

### Monitor Thing

The following configuration parameters are available on the Monitor thing:

| Parameter | Parameter ID | Required/Optional | Description |
|-----------|--------------|-------------------|-------------|
| Monitor ID             | monitorId            | Required          | Id of monitor defined in Zoneminder. |
| Image Refresh Interval | imageRefreshInterval | Optional          | Interval in which snapshot image channel will be updated. |
| Alarm Duration         | alarmDuration        | Required          | How long the alarm will run once triggered by the triggerAlarm channel. |

## Channels

### Server Thing

| Channel  | Type   | Description  |
|----------|--------|--------------|
| imageMonitorId | String      | Monitor ID to use for selecting an image URL. Also, sending an OFF command to this channel will reset the monitor id and url to UNDEF.  |
| imageUrl       | String      | Image URL for monitor id specified by imageMonitorId. Channel is UNDEF if the monitor id is not set, or if an OFF command is sent to the imageMonitorId channel. |
| videoMonitorId | String      | Monitor ID to use for selecting a video URL. Also, sending an OFF command to this channel will reset the monitor id and url to UNDEF.  |
| videoUrl       | String      | Video URL for monitor id specified by videoMonitorId. Channel is UNDEF if the monitor id is not set, or if an OFF command is sent to the videoMonitorId channel. |

### Monitor Thing

| Channel  | Type   | Description  |
|----------|--------|--------------|
| id                | String      | Monitor ID  |
| name              | String      | Monitor name  |
| image             | Image       | Snapshot image  |
| enable            | Switch      | Enable/disable monitor  |
| function          | String      | Monitor function (e.g. Nodect, Mocord)  |
| alarm             | Switch      | Monitor is alarming  |
| state             | String      | Monitor state (e.g. IDLE, ALARM, TAPE)  |
| triggerAlarm      | Switch      | Turn alarm on/off  |
| hourEvents        | Number      | Number of events in last hour |
| dayEvents         | Number      | Number of events in last day  |
| weekEvents        | Number      | Number of events in last week  |
| monthEvents       | Number      | Number of events in last month  |
| yearEvents        | Number      | Number of events in last year  |
| totalEvents       | Number      | Total number of events  |
| imageUrl          | String      | URL for image snapshot  |
| videoUrl          | String      | URL for JPEG video stream  |
| eventId           | String      | Event ID  |
| eventName         | String      | Event name  |
| eventCause        | String      | Event cause  |
| eventNotes        | String      | Event notes  |
| eventStart        | DateTime    | Event start date/time |
| eventEnd          | DateTime    | Event end date/time  |
| eventFrames       | Number      | Event frames  |
| eventAlarmFrames  | Number      | Event alarm frames |
| eventLength       | Number:Time | Event length in seconds  |

## Thing Actions

### triggerAlarm

The `triggerAlarm` action triggers an alarm that runs for the number of seconds specified by the parameter `duration`.

##### triggerAlarm - trigger an alarm

```java
void triggerAlarm(Number duration)
```

```
Parameters:
duration - The number of seconds for which the alarm should run.
```

### triggerAlarm

The `triggerAlarm` action triggers an alarm that runs for the number of seconds specified
in the Monitor thing configuration.

##### triggerAlarm - trigger an alarm

```java
void triggerAlarm()
```

### triggerAlarmOff

The `triggerAlarmOff` action cancels a running alarm.

##### triggerAlarmOff - cancel an alarm

```java
void triggerAlarmOff()
```

### Requirements

The binding requires Zoneminder version 1.34.0 or greater, and API version 2.0 or greater.
The API must be enabled in the Zoneminder configuration using the **OPT_USE_API** parameter.

The binding can access Zoneminder with or without authentication.
If you have authentication enabled in Zoneminder, set the **user** and **pass** 
config paremeters in the *server* thing.

## Full Example

### Things

```
Bridge zm:server:server [ host="192.168.1.100", refreshInterval=5, defaultAlarmDuration=120, discoveryEnabled=true, useDefaultUrlPath=true ]

Thing zm:monitor:1 "Monitor 1" (zm:server:server) [ monitorId="1", imageRefreshInterval=10, alarmDuration=180 ]

Thing zm:monitor:2 "Monitor 2" (zm:server:server) [ monitorId="2", imageRefreshInterval=10, alarmDuration=180 ]
```

### Items

```
// Server
String ZmServer_ImageMonitorId "Image Monitor Id [%s]" { channel="zm:server:server:imageMonitorId" }
String ZmServer_ImageUrl "Image Url [%s]" { channel="zm:server:server:imageUrl" }
String ZmServer_VideoMonitorId "Video Monitor Id [%s]" { channel="zm:server:server:videoMonitorId" }
String ZmServer_VideoUrl "Video Url [%s]" { channel="zm:server:server:videoUrl" }

// Monitor
String      ZM_Monitor1_Id           "Monitor Id [%s]"              { channel="zm:monitor:1:id" }
String      ZM_Monitor1_Name         "Monitor Name [%s]"            { channel="zm:monitor:1:name" }
Image       ZM_Monitor1_Image        "Image [%s]"                   { channel="zm:monitor:1:image" }
Switch      ZM_Monitor1_Enable       "Enable [%s]"                  { channel="zm:monitor:1:enable" }
String      ZM_Monitor1_Function     "Function [%s]"                { channel="zm:monitor:1:function" }
Switch      ZM_Monitor1_Alarm        "Alarm Status [%s]"            { channel="zm:monitor:1:alarm" }
String      ZM_Monitor1_State        "Alarm State [%s]"             { channel="zm:monitor:1:state" }
Switch      ZM_Monitor1_TriggerAlarm "Trigger Alarm [%s]"           { channel="zm:monitor:1:triggerAlarm" }
Number      ZM_Monitor1_HourEvents   "Hour Events [%.0f]"           { channel="zm:monitor:1:hourEvents" }
Number      ZM_Monitor1_DayEvents    "Day Events [%.0f]"            { channel="zm:monitor:1:dayEvents" }
Number      ZM_Monitor1_WeekEvents   "Week Events [%.0f]"           { channel="zm:monitor:1:weekEvents" }
Number      ZM_Monitor1_MonthEvents  "Month Events [%.0f]"          { channel="zm:monitor:1:monthEvents" }
Number      ZM_Monitor1_TotalEvents  "Total Events [%.0f]"          { channel="zm:monitor:1:totalEvents" }
String      ZM_Monitor1_ImageUrl     "Image URL [%s]"               { channel="zm:monitor:1:imageUrl" }
String      ZM_Monitor1_VideoUrl     "Video URL [%s]"               { channel="zm:monitor:1:videoUrl" }
String      ZM_Monitor1_EventId      "Event Id [%s]"                { channel="zm:monitor:1:eventId" }
String      ZM_Monitor1_Event_Name   "Event Name [%s]"              { channel="zm:monitor:1:eventName" }
String      ZM_Monitor1_EventCause   "Event Cause [%s]"             { channel="zm:monitor:1:eventCause" }
DateTime    ZM_Monitor1_EventStart   "Event Start [%s]"             { channel="zm:monitor:1:eventStart" }
DateTime    ZM_Monitor1_EventEnd     "Event End [%s]"               { channel="zm:monitor:1:eventEnd" }
Number      ZM_Monitor1_Frames       "Event Frames [%.0f]"          { channel="zm:monitor:1:eventFrames" }
Number      ZM_Monitor1_AlarmFrames  "Event Alarm Frames [%.0f]"    { channel="zm:monitor:1:eventAlarmFrames" }
Number:Time ZM_Monitor1_Length       "Event Length [%.2f]"          { channel="zm:monitor:1:eventLength" }
```

### Sitemap


```
Selection item=ZmServer_ImageMonitorId
Image item=ZmServer_ImageUrl
Selection item=ZmServer_VideoMonitorId
Video item=ZmServer_VideoUrl url="" encoding="mjpeg"
                
Selection item=ZM_Monitor1_Function
Selection item=ZM_Monitor1_Enable
Image item=ZM_Monitor1_Image
```

### Rules

The following examples assume you have a motion sensor that is linked to an item called *MotionSensorAlarm*.

```
rule "Record When Motion Detected Using Channel"
when
    Item MotionSensorAlarm changed to ON
then
    ZM_TriggerAlarm.sendComand(ON)
end
```

```
rule "Record for 120 Seconds When Motion Detected"
when
    Item MotionSensorAlarm changed to ON
then
    val zmActions = getActions("zm", "zm:monitor:1")
    zmActions.triggerAlarmOn(120)
end
```

```
rule "Record When Motion Detected"
when
    Item MotionSensorAlarm changed to ON
then
    val zmActions = getActions("zm", "zm:monitor:1")
    zmActions.triggerAlarmOn()
end
```

```
rule "Record When Motion Detection Cleared"
when
    Item MotionSensorAlarm changed to OFF
then
    val zmActions = getActions("zm", "zm:monitor:1")
    zmActions.triggerAlarmOff()
end
```

```
val int NUM_MONITORS = 6
var int monitorId = 1

rule "Rotate Through All Monitor Images Every 10 Seconds"
when
    Time cron "0/10 * * ? * * *"
then
    var String id = String::format("%d", monitorId)
    ZmServer_ImageMonitorId.sendCommand(id)
    monitorId = monitorId + 1
    if (monitorId > NUM_MONITORS) {
        monitorId = 1
    }
end
```
