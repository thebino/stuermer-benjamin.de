---
layout: post
title: "CI für Android (1/5) – Allgemein"
date: 2012-10-28 12:06:45 +0200
comments: false
sharing: false
categories: Android
---
<h2>Einführung</h2>
<br />
<p>Im Jahre 2005 meldete der Flugzeughersteller Airbus den Medien, dass sich die Auslieferung ihres A380 um einige Monate verzögern wird. Ganze Rumpfteile, die in der ganzen Welt gefertigt werden, können nicht zusammen gefügt werden, da die Kabelverbindungen zu kurz seien. Nachforschungen stellten hinterher heraus, dass eine unterschiedliche Versionsnummer der CAD Software zu dem Fehler führte.</p>
<br />
<p>Diese Last-Minute-Integration kostete Airbus zwei Milliarden Dollar und eine Auslieferungsverschiebung von neun Monaten.</p>
<br />
<!-- more -->
<h2>Was ist Continuous Integration</h2>
<br />
<p>Der Begriff stammt aus der Software Entwicklung und bedeutet so viel wie ständiges/kontinuierliches Integrieren. In der heutigen Zeit arbeiten in den unterschiedlichsten Bereichen und Projekten Weltweit meist ganze Gruppen. Deshalb kann zwar jeder einzelne dafür sorgen, dass sein Teil der Arbeit möglichst fehlerfrei ausgeführt wird, jedoch kann niemand garantieren, dass das Gesamtkonstrukt am Ende fehlerfrei arbeitet. Ob das in der Einführung genannte Kabel das Problem ist oder einzelne Module in einer Software, spielt dabei eigentlich keine Rolle.</p>
<br />
<p>CI wie es in der Kurzform genannt wird, soll hier Abhilfe schaffen. Jedes mal wenn ein einzelner Entwickler einen Schritt näher an sein Ziel gelangt, wird seine Arbeit “eingecheckt” und mit Hilfe von automatischen Programmen im Gesamtsystem geprüft. Das sog. “einchecken” kann hierbei über die unterschiedlichsten Wege passieren, etwa in dem er es an seinen Vorgesetzten übergibt oder in einem Versions Controll System speichert.</p>

![image-title-here](/images/posts/2012-10-28_defect_chart.gif){:class="img-responsive"}
http://www.agitar.com/solutions/why_unit_testing.html