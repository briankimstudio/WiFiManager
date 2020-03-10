## Current development going on here :arrow_right: [Development Branch](https://github.com/tzapu/WiFiManager/tree/development)

# WiFiManager

WiFiManager with EspAsyncWebserver on ESP8266

This is based on works from https://github.com/tzapu/WiFiManager (V0.15) and https://github.com/btomer/WiFiManager.

Observations while working on this code,

1. WiFi.scanNetworks() call returns nothing when it is called within async web handler. As a result, no SSIDs will show up.
2. After deleting WiFiManager instance, our own web server fails in binding same web port occasionally. It seems that TCP port is not released clearely. 

Work arounds included in this code,

1. Call async version of scanNetworks() in advance. The result will be available when async web handler needs it.
2. Once WiFiManager stores SSID, PASSWD from user, it reboots. Then, WiFiManager won't need to start its own webserver anymore, which means our own web server won't have troulb in binding web port.

These issues need to be investigated further for fundemental solutions.