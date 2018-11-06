---
layout: post
title: Multiseat with Ubuntu
date: 2012-03-02 22:44:54 +0200
comments: false
sharing: false
categories: Linux
---

img left /images/posts/2012-03-02_dualhead.jpg
Seit gestern läuft für Ubuntu 12.04 LTS die Betaphase. Für mich der geeignete Zeitpunkt mein Multiseat von 10.04 upzudaten.

Zusätzlich werden einige Hardwareänderungen vorgenommen. Somit ergibt sich folgende Hardware zusammenstellung:

Asus Rampage Extreme II
Core i7-920
6 GB DDR3 – 1066
GeForce 8800 GT
GeForce 8400 GS
Intel X25-SSD

Als Grundlage habe ich die Ubuntu 12.04 Server DVD genommen, sollte aber mit der Desktop Version ebenfalls funktionieren.

<!-- more -->

Gleich zu beginn dürfte auffallen, dass wir nun weder mit KDM noch mit GDM arbeiten. Der Grund hierfür ist, dass der GDM seit der Version 11.04 durch LightDM ersetzt wurde. Dabei handelt es sich um einen schlanken und dennoch leistungsstarken Nachfolger von GDM.


{% highlight shell lineos %}
apt-get install lightdm
{% endhighlight %}
Der LightDM bietet mit seiner Flexiblen Struktur eine sehr einfache Unterstützung des Multiseat verfahrens, hier die notwendige Konfiguration:

[/etc/lightdm/lightdm.conf]
{% highlight shell %}
[SeatDefaults]
 
# Unity
greeter-session=unity-greeter
user-session=ubuntu
 
[Seat:0]
xserver-command=/usr/bin/X -config xorg_seat1.conf -nolisten tcp -isolateDevice PCI:3:0:0 vt7
 
[Seat:1]
xserver-command=/usr/bin/X -config xorg_seat2.conf -nolisten tcp -isolateDevice PCI:2:0:0 -sharevts
Nun benötigen wir ein paar Systeminformationen, um mit der Konfiguration der Xserver-Layouts fortzufahren:
{% endhighlight %}

{% highlight shell lineos %}
root@Operator:~# lspci | grep VGA
02:00.0 VGA compatible controller: nVidia Corporation G84 [GeForce 8600 GT] (rev a1)
03:00.0 VGA compatible controller: nVidia Corporation G98 [GeForce 8400 GS] (rev a1)
{% endhighlight %}
Nun noch Tastatur und Maus


{% highlight shell lineos %}
root@Operator:~# ls /dev/input/by-id/ | grep mouse
usb-HOLTEK_Wireless_Keyboard_Mouse_2.4G_-event-mouse
usb-HOLTEK_Wireless_Keyboard_Mouse_2.4G_-if01-event-mouse
usb-HOLTEK_Wireless_Keyboard_Mouse_2.4G_-if01-mouse
usb-HOLTEK_Wireless_Keyboard_Mouse_2.4G_-mouse
usb-Logitech_USB-PS_2_Optical_Mouse-event-mouse
usb-Logitech_USB-PS_2_Optical_Mouse-mouse
usb-Logitech_USB_Receiver-event-mouse
usb-Logitech_USB_Receiver-if01-event-mouse
usb-Logitech_USB_Receiver-if01-mouse
usb-Logitech_USB_Receiver-mouse
{% endhighlight %}

{% highlight shell lineos %}
root@Operator:~# ls /dev/input/by-id/ | grep kbd
usb-HOLTEK_Wireless_Keyboard_Mouse_2.4G_-event-kbd
usb-Logitech_Logitech_USB_Keyboard-event-kbd
usb-Logitech_USB_Receiver-event-kbd
{% endhighlight %}
Um nun jedem Seat seine Maus und Tastatur zuweisen zu können, verwenden wir udev-Regeln:

[/etc/udev/rules.d/99-seat1.conf]
{% highlight vim %}
SUBSYSTEM=="input", ENV{ID_INPUT.tags}="input_seat1"
{% endhighlight %}

[/etc/udev/rules.d/99-seat2.conf]
{% highlight vim %}
SUBSYSTEM=="input", ATTRS{idProduct}=="C01E", ENV{ID_INPUT.tags}="input_seat2"
SUBSYSTEM=="input", ATTRS{idProduct}=="C30F", ENV{ID_INPUT.tags}="input_seat2"
SUBSYSTEM=="input", ATTRS{idProduct}=="c01e", ENV{ID_INPUT.tags}="input_seat2"
{% endhighlight %}
Wenn wir nun lightdm starten sollten zwei Instanzen des X Servers laufen:


{% highlight shell lineos %}
<em>root@Operator:~# ps aux | grep X</em>
root     12397  0.0  0.0  67588  2720 tty8     Ss+  08:07   0:00 /usr/bin/X -config xorg_seat1.conf -nolisten tcp -isolateDevice PCI:3:0:0 vt7 :0 -auth /var/run/lightdm/root/:0 -nolisten tcp vt7 -novtswitch -background none
root     12758  0.0  0.2 142932 14848 tty7     Ss+  08:08   0:00 /usr/bin/X -config xorg_seat2.conf -nolisten tcp -isolateDevice PCI:2:0:0 -sharevts :1 -auth /var/run/lightdm/root/:1 -nolisten tcp vt8 -novtswitch
{% endhighlight %}