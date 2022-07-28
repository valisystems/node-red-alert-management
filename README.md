# node-red-alert-management
Node-red alert management software


### Abbreviations used:
  - RPI -> RPi micro controller unit, single board
  - API -> application program interface
  - HTTP -> HypeText Transfer Protocol
  - URL -> Uniform Resource Locator
  - MAC -> Media Access Control


## Flow 1

Process incoming URL API request to set the RPI pin state. This Flow is adjusted to set the state of Pin 40, and it can be used as an example to set the state of any available RPI pin. For instance, in Flow 5 we have two logical branches to set Pin 40 and Pin 38.

Static password is set for minimal security, to prevent unwanted messages.

Sample API request, 

http://hostaddress/control2?authent=abcdef&gpio=40&turn=on

![nodered_flow_1](https://user-images.githubusercontent.com/53027462/61923756-4687cd80-af8f-11e9-9a34-50924e20dbf8.png)


## Flow 2

Process pin state to a HTTP URL request on a EMS LvMonitor System. When pin state changes 0 -> 1 or 1 -> 0, the current flow processes this change and depending on the current state of the pin it generates an appropriate HTTP URL request to a EMS LvMonitor System. 

This is primarily used to generate an event with a type Alarm or Normal, state 0 of a pin represents event type Normal and state 1 of a pin represents event type Alarm.

![nodered_flow_2](https://user-images.githubusercontent.com/53027462/61923757-47206400-af8f-11e9-9946-9625c96305fe.png)


## Flow 3

Process button pressed event, either from the physical board or the dashboard interface. The flow uses pin name and state to generate a HTTP URL request to a EMS LvMonitor System. Similar to the second flow, the generated HTTP URL request represents an event with a type Alarm or Normal.

There are currently activated two pins in this flow, Pin 7 and Pin 11, and three available buttons that are accessible from the dashboard, Alarm 7, Alarm 11 and Cancel. Alarm 7 sends a HTTP URL request for Pin 7 with event type Alarm, Alarm 11 does similar for Pin 11 and Cancel sends event type Normal for both Pins 7 and 11.

There is a parallel action in this flow, that is completed once after the boot up cycle, MAC address is fetched and set into a global variable for later usage in this flow as the BaseName parameter value for HTTP URL requests to EMS LvMonitor System.

Buttons are accessed from the Dashboard interface, http://hostaddress/ui and selecting Controlledcare Station Pin from the menu.

![nodered_flow_3](https://user-images.githubusercontent.com/53027462/61923758-47206400-af8f-11e9-926c-f99bbf96f419.png)


## Flow 4
Process incoming URL API request to generate an event sent via URL HTTP request to a EMS LvMonitor System. These can be requests sent from door locks, cameras, card readers and any other technologies with an available HTTP URL request mechanism.

The incoming request is processed, and an appropriate outgoing request is prepared. A sample request,

http://hostaddress/new/?mac=000237aef72b&status=1&from=bath&room=101

![nodered_flow_4](https://user-images.githubusercontent.com/53027462/61923759-47206400-af8f-11e9-9b28-bd97d3ee0f78.png)


## Flow 5
Process incoming URL API request to set the RPI pin state. This Flow is created based on the sample Flow 1, and just expanded to support Pin 38 and Pin 40 with an appropriate signal states passed to the Dashboard.

Static password is set for minimal security, to prevent unwanted messages.

Sample API request, 

http://hostaddress/control?authent=abcdef&gpio=40&turn=on

Current pin state can be viewed by accessing the Dashboard interface, http://hostaddress/ui and selecting Controlledcare Station URL from the menu.

![nodered_flow_5](https://user-images.githubusercontent.com/53027462/61923760-47b8fa80-af8f-11e9-967a-3d83e94dbd79.png)

![nodered_dashboard_pin](https://user-images.githubusercontent.com/53027462/61923761-47b8fa80-af8f-11e9-94ee-93f0a4744ee5.png)

![nodered_dashboard_url](https://user-images.githubusercontent.com/53027462/61923755-4687cd80-af8f-11e9-9f0e-a669262d63ba.png)
