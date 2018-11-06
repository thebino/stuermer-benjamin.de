---
layout: post
title: "Raspberry Pi"
date: 2012-07-16 23:04:54 +0200
comments: false
sharing: false
categories: [ Raspberry Pi, Linux ]
---
Bei dem Raspberry Pi handelt es sich zwar nicht um den kleinsten, aber definitiv zurzeit um den billigsten Linux Computer.

![image-title-here](/images/posts/2012-07-16_Raspberry.jpeg){:class="img-responsive"}

Für gerade einmal 35 USD (28 Euro) erhält man ein Exemplar. Entwickelt wurde der Raspberry Pi in England durch die Raspberry Pi Foundation. Unterstützt wird diese unter anderem durch die Britische Regierung um den landesweiten Mangel an IT-Fachkräften zu unterbinden.

<!-- more -->

Betrieben wird der Miniatur Computer mit Hilfe einer 12V Spannungsversorgung über einen Mini-USB Stecker.

Als Betriebssystem bieten die Hersteller unterschiedliche Linux Distributionen an.
Dieses wird auf eine SD Karte geschrieben und von dort gebootet.

Eine Liste mit verschiedenen Betriebssystemen für den Pi findet sich unter elinux.org.

Schicke Gehäuse findet man unter anderem bei Adafruit ebenso wie ein 2″ oder 3,5″ Display. Besonderes Augenmerkt richten Experten auf die GPU. Trotz Linux Grundsatz kommt ein Propritärer Treiber zum Einsatz. Nichts desto trotz spielt diese GPU sogar Full-HD Filme ruckelfrei ab und unterstützt OpenGL ES 2.0 und H.264

Überspielen lässt sich das Betriebssystem Image mit dem dd Tool


{% highlight shell lineos %}
dd bs=1m if=debian6-19-04-2012.img of=/dev/rdiskX
{% endhighlight %}
Nach der Installation sollte die SD Karte noch korrekt partitioniert werden, das Standardsystem ist lediglich auf 2 GB Karten ausgelegt


{% highlight shell lineos %}
fdisk -c -u /dev/mmcblk0
{% endhighlight %}
“den Partitionierer fdisk startet. Mit “p” erhält man einen Überblick über die bestehenden Partitionen; merken Sie sich den Wert für den Start der zweiten Partition (bei dem aktuellen Image vom 19.4. ist das 157696). Zunächst löscht man mit “d” die Partitionen 3 und 2, dann legt man mit “n” eine neue primäre Partition 2 an. Als Startwert verwendet man den Startwert der alten Partition 2, für das Ende akzeptiert man mit “Enter” den Vorschlag von fdisk. “w” schreibt die neue Partitionierung auf die Karte. Nach einem Reboot und erneuter Anmeldung wird dann das Dateisystem mit


{% highlight shell lineos %}
resize2fs /dev/mmcblk0p2
{% endhighlight %}
vergrößert.

Nun kann man mit startx den schlanken LXDE-Desktop starten, der in seinem Startmenü diverse Anwendungen anbietet und sich durchaus flüssig bedienen lässt.”

http://www.spiegel.de/netzwelt/gadgets/raspberry-pi-guenstigster-linux-computer-als-media-center-a-842581.html

 

System auf Deutsch umstellen

{% highlight shell lineos %}
sudo dpkg-reconfigure locales
{% endhighlight %}
Nachdem unsere Tastatur der deutschen Sprache mächtig ist, legen wir uns am besten einen eigenen User auf dem System an.

 

Eigenen User Anlegen

{% highlight shell lineos %}
$ sudo adduser max
$ sudo adduser max admin
$ sudo apt-get install openssh-server
$ passwd max
{% endhighlight %}
Nun ist ein Login auch per SSH und eigenem User möglich.

 

Eigene Distribution erstellen
Möchte man eine eigene Distribution bauen, empfehlen einige Seiten das OpenELEC Projekt

Als Multimedia System empfiehlt es sich, XBMC zu nutzen, hierzu haben die Offiziellen XBMC Entwickler ein eigenes System samt Installer entwickelt. Dieses befindet sich seit Mai 2012 zwar erst im Beta Stadium, macht jedoch jetzt schon einen sehr guten Eindruck Als bedienung empfiehlt sich XBMC Remote auf dem Handy zu installieren, dies ist sowohl für Android als auch Apple Devices verfügbar.

Aprospos Android, dies ist ebenfalls als Betriebssystem lauffähig. Unter elinux.org#Android wie auch unter lesderid.net finden sich ein Images dazu.

 

Emulator
Wer es nicht mehr erwarten kann, bis seine Himbeere reif ist, kann sich mit Hilfe von qemu (einem opensource emulator) eine virtuelle Kopie seines zuküftigen Systems erstellen.