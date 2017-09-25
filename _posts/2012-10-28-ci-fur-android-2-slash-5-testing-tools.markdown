---
layout: post
title: "CI für Android (2/5) – Testing Tools"
date: 2012-10-28 16:51:47 +0200
comments: false
sharing: false
categories: Android
---
Nach einer kleinen Einführung im ersten Teil schauen wir uns hier mal ein Tools an, mit denen wir automatische Tests erstellen können.



Dazu gehen wir näher auf folgende Tools ein:

Android Testing Framework
Robotium
Roboelectric

Android Testing Framework
Das Android Testing Framework, ist bereits im Android-SDK enthalten und auch in der Offiziellen Dokumentation ausführlich behandelt.

Zusätzlich zu unserem “zu testenden Projekt” erstellen wir ein Android Test Project


{% img /images/posts/2012-10-28_test_framework.jpg %}

<!-- more -->


Bei der Wahl des Projektnamen ist es sinnvoll, an das zu testende Projekt ein “Test” anzuhängen. z.B.: ExampleView  –> ExampleViewTest

In der Offiziellen Dokumentation wird zusätzlich dazu geraten, das root Verzeichnis des TestProjekts innerhalb der ExampleView zu platzieren. Dadurch bleiben die App wie auch der Test Code immer beieinander.


{% img /images/posts/2012-10-28_ordner_struktur.jpg %}


Erstellen wir nun unseren ersten Test Case
New -> JUnit Test Case

{% img /images/posts/2012-10-28_test_case.jpg %}



Mit Hilfe der Methoden
{% codeblock lang:java %}
public void sendKeys (int… keys)
public static void assertTrue (boolean condition)
{% endcodeblock %}
lassen sich aus JUnit gewohnte TestCases erstellen. Eine Ausführliche Einführung finden Sie auf der Seite tutsplus.com

 

Robotium
Mit Robotium lässt sich das Android Testing Framework um einige Funktionen erleichtern. Beispielsweise erspart sich der Tester das Starten des Emulators wie auch der entsprechenden Anwendung.

Mit Robotium lassen sich neben der üblichen AssertEquals auch Android Toasts, Activities, Menüs und Kontext Menüs bedienen wie auch auslesen.


Weitere Informationen finden sich unter anderem auf der Offiziellen Projektseite.

 

Roboelectric
Während Robotium auf Instrument Testing ala JUnit 3 zurück greift, arbeitet Roboelectric mit non-Instrument JUnit 4 Methoden.

Das Testen mit Roboelectric ist spürrbar schneller, jedoch nach Aussage nicht 100% akkurat  was die Android API angeht.

Sowohl die Offizielle Projektseite bietet reichhaltige Informationen und Beispiele als auch unter vogella.de wird man wiedermal ausführlich mit wunderbaren Tutorials bedient.