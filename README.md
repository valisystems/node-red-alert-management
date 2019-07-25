# node-red-alert-management
Node-red alert management software


### Abbreviations used:
  - RPI -> Raspberry Pi
  - API -> application program interface
  - HTTP -> HypeText Transfer Protocol
  - URL -> Uniform Resource Locator
  - MAC -> Media Access Control


## Flow 1

Process incoming URL API request to set the RPI pin state. This Flow is adjusted to set the state of Pin 40, and it can be used as an example to set the state of any available RPI pin. For instance, in Flow 5 we have two logical branches to set Pin 40 and Pin 38.

Static password is set for minimal security, to prevent unwanted messages.

Sample API request, 

http://hostaddress/control2?authent=abcdef&gpio=40&turn=on


## Flow 2

Process pin state to a HTTP URL request on a EMS LvMonitor System. When pin state changes 0 -> 1 or 1 -> 0, the current flow processes this change and depending on the current state of the pin it generates an appropriate HTTP URL request to a EMS LvMonitor System. 

This is primarily used to generate an event with a type Alarm or Normal, state 0 of a pin represents event type Normal and state 1 of a pin represents event type Alarm.


## Flow 3

Process button pressed event, either from the physical board or the dashboard interface. The flow uses pin name and state to generate a HTTP URL request to a EMS LvMonitor System. Similar to the second flow, the generated HTTP URL request represents an event with a type Alarm or Normal.

There are currently activated two pins in this flow, Pin 7 and Pin 11, and three available buttons that are accessible from the dashboard, Alarm 7, Alarm 11 and Cancel. Alarm 7 sends a HTTP URL request for Pin 7 with event type Alarm, Alarm 11 does similar for Pin 11 and Cancel sends event type Normal for both Pins 7 and 11.

There is a parallel action in this flow, that is completed once after the boot up cycle, MAC address is fetched and set into a global variable for later usage in this flow as the BaseName parameter value for HTTP URL requests to EMS LvMonitor System.

Buttons are accessed from the Dashboard interface, http://hostaddress/ui and selecting Controlledcare Station Pin from the menu.


## Flow 4
Process incoming URL API request to generate an event sent via URL HTTP request to a EMS LvMonitor System. These can be requests sent from door locks, cameras, card readers and any other technologies with an available HTTP URL request mechanism.

The incoming request is processed, and an appropriate outgoing request is prepared. A sample request,

http://hostaddress/new/?mac=000237aef72b&status=1&from=bath&room=101


## Flow 5
Process incoming URL API request to set the RPI pin state. This Flow is created based on the sample Flow 1, and just expanded to support Pin 38 and Pin 40 with an appropriate signal states passed to the Dashboard.

Static password is set for minimal security, to prevent unwanted messages.

Sample API request, 

http://hostaddress/control?authent=abcdef&gpio=40&turn=on

Current pin state can be viewed by accessing the Dashboard interface, http://hostaddress/ui and selecting Controlledcare Station URL from the menu.
