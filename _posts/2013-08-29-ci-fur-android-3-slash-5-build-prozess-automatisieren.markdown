---
layout: post
title: "CI für Android (3/5) – Build Prozess automatisieren"
date: 2013-08-29 16:52:03 +0200
comments: false
sharing: false
categories: Android
---
<p>Was für c/c++ Sourcen "make" erledigt, wird in der Java Welt mit Ant gemacht. Seit Sommer 2013 kommt hier nun auch noch Gradle hinzu.</p>
<div class="youtube"><object width="350" height="300" classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,40,0"><param name="wmode" value="transparent" /><param name="src" value="http://www.youtube.com/v/LCJAgPkpmR0?autoplay=0" /><embed width="350" height="300" type="application/x-shockwave-flash" src="http://www.youtube.com/v/LCJAgPkpmR0?autoplay=0" wmode="transparent" /></object></div>
<p>Während für Gradle zwei komplett neue Plugins geschaffen wurden (android und android-library) bedient sich Apache Ant gewohnter Methoden um aus Programmcode ausführbare Software-Packete zu erstellen.<br />
Im ersten Schritt werden wir mit Ant Skripten unseren Java Sourcen automatisch in eine ausführbare .apk umwandeln.</p>
<br />

<p>Durch diese Automatisierten Skripte sparen wir uns künftig nicht nur Zeit, weil sich um den Kompilierungsprozess sich kein Entwickler selbst kümmern muss, wir schaffen auch ein stück weit Reproduzierbarkeit.</p>
<br />

<p>Da das Skript direkt mit dem Source gespeichert wird, kann zu jedem Zeitpunkt eine identische Binär Version erstellt werden.</p>
<br />

<p>ANT wird zwar sowohl von Eclipse als auch vom ADT* verwendet, der Nutzer bekommt hiervon jedoch nichts mit. <span>*ADT bassiert auf dem Eclipse Code</span></p>
<br />

<!-- more -->

<p>Im von Google 2013 vorgestellten Android Studio können ebenfalls ANT Skripte zur Ausführung genutzt werden, es wird jedoch zum Umstieg auf die Gradle Buildfiles geraten.</p>
<br />

<p>Für unser Continuous Integration planen wir einen bestimmten Prozess Ablauf, um diesen umsetzen zu können hält Apache Ant ein Paket von über 150 Tasks bereit. Uns werden besonders folgende Task von nutzen sein:</p>
<br />

<ol>
<li>javac zum Kompilieren</li>
<li>copy zum Kopieren</li>
<li>delete zum Löschen</li>
<li>junit für automatisierte (JUnit-)Tests.</li>
<li>exec zum Ausführen von System-Programmen</li>
<li>zip zum Zippen</li>
</ol>

<h2>Die build.xml</h2>
<br />
<p>Gesteuert wird Ant durch eine zentrale Build-Datei (build.xml), Android unterstützt uns bei der Erstellung.</p>
<p>android update project --name "Mein Projekt" --path . --target "Google Inc.:Google APIs:14"<br />
android update test-project --path ./tests --main ../</p>
<br />

<p>Der obere Befehl erstellt eine build.xml für unser Projekt. Wird mit Library Projekten gearbeitet, müssen diese auf gleiche Weise in den Build-Prozess gelangen.<br />
<p>Direkt unter unserem Projekt wird das Test Projekt hinzugefügt, die Reihenfolge spielt dabei keine Rolle.</p>
<p>Am sinnvollsten ist es, diese Befehle in einem Shell oder Python Script zu kapseln, so lassen sich diese jederzeit erweitern und können mit dem Projekt Source verwaltet werden.</p>
<br />

<h2>Ant Debug / Release</h2>
<br />

<p>Damit nun aus unserem Source Code und der build.xml eine fertige APK werden kann, müssen wir diese noch mit Ant behandeln. Um alle möglichen Prozesse von Ant zu erhalten, können Sie auf der Konsole in das Projekt Verzeichnis wechseln und dort den Befehl "ant" eingeben.</p>
<br />
{% highlight shell lineos %}
$ ant
Buildfile: DemoApp/App-Code/DemoProjekt/build.xml
help:
 [echo] Android Ant Build. Available targets:
 [echo] help: Displays this help.
 [echo] clean: Removes output files created by other targets.
 [echo] This calls the same target on all dependent projects.
 [echo] Use 'ant nodeps clean' to only clean the local project
 [echo] debug: Builds the application and signs it with a debug key.
 [echo] The 'nodeps' target can be used to only build the
 [echo] current project and ignore the libraries using:
 [echo] 'ant nodeps debug'
 [echo] release: Builds the application. The generated apk file must be
 [echo] signed before it is published.
 [echo] The 'nodeps' target can be used to only build the
 [echo] current project and ignore the libraries using:
 [echo] 'ant nodeps release'
 {% endhighlight %}

<p>Neben clean, debug und release finden sich noch Tasks für das Testing und zum de-/installieren der unterschiedlichsten Packages.</p>
<br />

<p>Mit dem Befehl "ant debug" wird nun in unserem Projektverzeichnis unter "bin/" ein lauffähiges APK erstellt. Dieses können Sie Beispielsweise per ADB auf ihr Mobile Device installieren.</p>
