---
layout: post
title: Ubuntu Nvidia API mismatch
date: 2009-09-08 07:51:22 +0200
comments: false
sharing: false
categories: Linux
---
Gelegentlich kann es beim Updaten des Kernels zu folgender Fehlermeldung kommen:

<!-- more -->

{% codeblock lang:sh %}
[ 39.753267] NVRM: API mismatch: the client has the version 260.19.44, but
[ 39.753268] NVRM: this kernel module has the version 260.19.06. Please
[ 39.753269] NVRM: make sure that this kernel module and all NVIDIA driver
[ 39.753270] NVRM: components have the same version.
{% endcodeblock %}

Diese sagt aus, dass die installierte Version des Kernel Moduls nicht mit der Version des Kernels kompatibel ist.

In einigen Fällen reicht es aus, das Modul zu löschen und die aktualisierte Version zu laden:

{% codeblock lang:sh %}rmmod nvidia
modprobe nvidia
anschließend muss der Display Manager (gdm oder kdm) neu gestartet werden:
{% endcodeblock %}


{% codeblock lang:sh %}
/etc/init.d/gdm restart
{% endcodeblock %}
oder
{% codeblock lang:sh %}
/etc/init.d/kdm restart
{% endcodeblock %}

Falls der Zustand beim nächsten Systemreboot erneut auftreten sollte, muss das installierte Nvidia Modul durch eine aktuelle Version ersetzt werden.

{% codeblock lang:sh %}
sudo apt-get install nvidia-current
{% endcodeblock %}