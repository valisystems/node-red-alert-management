# Change Log

## [1.0.0] - 05-02-2019
- Modified Flow 3, added mechanism to grab the system's MAC address and use it as a global variable
- Added Dashboard interface to view pin states in Flow 5
- Added Dashboard interface to send Alarm, Normal or Cancel events for Flow 3
- Modified Flow 3, integrated events from Dashboard and modified generated HTTP URL requests to use EMS LvMonitor system API structure
- Modified Flow 5, integrated Dashboard pin states

## [0.4.0] - 01-06-2019
- Renamed Flow 3 -> Flow 4 and Flow 4 -> Flow 5
- Added Flow 3, that processes button press action and generates an appropriate HTTP URL request to EMS LvMonitor system, currently using static MAC address in the request

## [0.3.0] - 11-14-2018
- Added Flow 3, that processes an incoming HTTP URL request and translates it to a EMS LvMonitor system URL Debug structure
- Added Flow 4, that is created using the structure of Flow 1, added an additional pin to control, Pin 38. Sample url http://hostaddress/control?authent=abcdef&gpio=38&turn=off

## [0.2.0] - 09-28-2018
- Modified Flow 1, added secret key to the HTTP URL request requirement, to prevent unwanted requests, sample url is http://hostaddress/control2?authent=abcdef&gpio=40&turn=on
- Modified Flow 2, added additional pin 11 to monitor, changed the structure of a generated HTTP URL request to a EMS LvMonitor system type

## [0.1.0] - 06-06-2018
- Added Flow 1, that processes an incoming HTTP URL request and changes state of pin according to the state in the request, sample URL http://hostaddress/control2?gpio=40&turn=on. Supported options for key 'turn' are 'on' and 'off', and static pin has been configured Pin 40.
- Added Flow 2, that monitors state of pin 7 and generates a HTTP URL request
