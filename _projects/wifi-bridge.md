---
title: WIFI Bridge with UMTS Fallback
layout: project
colors:
  - color: FF5722
  - color: E64A19
  - color: FFCCBC
  - color: 607D8B
images:
  - overview: /images/project_timetracker.png
---

Hardware: 
- alix 3d3 (PC Engines)[https://www.pcengines.ch/alix3d3.htm]
- Compex WLM54GP23 (1000 mW - 30 dBm)
- 7db antennas

Software:
- OpenWrt 15.05.1


# WiFi-to-WiFi Bridge
A WiFi Bridge connects two different wireless networks as if they are only one network.




# Access Point or Hotspot
Allows WiFi devices to connect to a wired network. A Hotspot is a special type of hotspot where people may obtain Internet access.


# WiFi Repeater
Extend an existing WiFi Signal from a wireless router or access point to devies outside the range of the origin router or access point.




# UMTS Dongle
## Required Packages
Install required packages via webinterface or command line `opgk install <package>`
- comgt 
- kmod-usb-serial 
- kmod-usb-serial-option 
- kmod-usb-serial-wwan 
- kmod-usb-acm usb-modeswitch 
- luci-proto-3g



```
gcom -d /dev/ttyUSB2 info
##### Wireless WAN Modem Configuration #####
Product text:
====

====
Manufacturer:           IMEI and Serial Number: comgt 20:04:54 -> -- Error Report --
comgt 20:04:54 -> ---->                       ^
comgt 20:04:54 -> Error @776, line 45, String is shorter than second argument. (7)
```


vi /etc/chatscripts/3g.chat
```
ABORT   BUSY
ABORT   'NO CARRIER'
ABORT   ERROR
REPORT  CONNECT
TIMEOUT 10
""      "AT&F"
""      "AT+CSQ"
OK      "ATE1"
OK      'AT+CGDCONT=1,"IP","$USE_APN"'
SAY     "Calling UMTS/GPRS"
TIMEOUT 30
OK      "ATD*99***1#"
CONNECT ' '
```

