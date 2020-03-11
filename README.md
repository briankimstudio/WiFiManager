# WiFiManager

WiFiManager with EspAsyncWebserver on ESP8266

This is based on works from https://github.com/tzapu/WiFiManager (V0.15) and https://github.com/btomer/WiFiManager.

Observations while working on this code,

1. WiFi.scanNetworks() call returns nothing when it is called within async web handler. As a result, no SSIDs will show up.
2. After deleting WiFiManager instance, our own web server fails in binding the same web port occasionally. It seems that TCP port is not released clearly and it may be in TIMED-WAIT state.

Workarounds included in this code,

1. Call async version of WiFi.scanNetworks() in advance. The result will be available when async web handler needs it.
2. Once WiFiManager stores SSID, PASSWORD from user, reboot ESP8266 immediately. Then, WiFiManager won't need to start its own web server anymore, which means our own web server won't have trouble in binding web port.

These issues need to be investigated further for fundamental solutions.