---
layout: post
title: "CI für Android (4/5) – Jenkins"
date: 2013-08-29 16:52:13 +0200
comments: false
sharing: false
categories: Android
---
<p>Nachdem wir im <a title="CI für Android (1/5) – Allgemein" href="http://www.stuermer-benjamin.de/v12_1/ci-fur-android-continuous-integration-allgemein/"><span style="color: #000000;">ersten Teil Continuous Integration</span></a> im allgemeinen behandelt haben, <a title="CI für Android (2/5) – Testing Tools" href="http://www.stuermer-benjamin.de/v12_1/ci-fur-android-25-tools-fur-automatisierung/"><span style="color: #000000;">der zweite Teil </span></a>unterschiedliche Testing Tools für Android angeschnitten hat, wollen wir nach<a title="CI für Android (3/5) – Build Prozess automatisieren" href="http://www.stuermer-benjamin.de/v12_1/ci-fur-android-35-build-prozess-automatisieren/"><span style="color: #000000;"> dem dritten Teil</span></a> über automatisierte Buildprozesse nun endlich zum Herz Stück von Continuous Integration kommen.</p>
<br />

<!-- more -->

<p>Um Continuous Integration für Android umsetzen zu können, könnten wir nun nach jeder Änderung im Source Code ein 'ant debug' ausführen und die App von Hand testen. Da dies immer noch einige Zeit in Anspruch nimmt nehmen wir uns einfach einen Butler. Im ganz speziellen einen Jenkins.</p>
<br />

<p>Bei Jenkins handelt es sich um eine Server Software, die genau für unsere gewünschten Ansprüche erstellt wurde. Wir teilen dem Jenkins vorher mit, zu welchen Zeitpunkten er was mit unserem Source Code machen soll.</p>
<br />

<ul>
 <li><span>Nach jedem Commit</span></li>
 <li>Zu festen Uhrzeiten</li>
 <li>Nach erfolgreichem Build</li>
 <li>etc.</li>
</ul>
<br />

<p>Für den Anfang währen Beispielsweise folgende Builds sinnvoll</p>
<br />

<span>Build einer Debug.apk nach jedem Commit</span>

<ul>
<li>Warnung per Mail wenn der Build Fehlschlägt</li>
<li>Ausführen von Instrumentation Tests bei erfolgreichem Build</li>
</ul>
<br />

<p>Die Installation und Einrichtung eines Jenkins habe ich <a title="Jenkins und das Android Plugin" href="http://www.stuermer-benjamin.de/v12_1/jenkins-und-das-android-plugin/"><span style="color: #000000;">in diesem Tutorial</span></a> zusammen gefasst</p>

<h2>Jenkins Android Job einrichten</h2>
<br />

<p>Wählen Sie <em>Neuen Job anlegen</em>, tragen einen Projektnamen ein und wählen <em>"Multikonfigurationsprojekt bauen"</em></p>
<br />

<p>Im Bereich "Source-Code-Management" wählen Sie nun Git und tragen ihre "Git Repository URL" ein. (Sollten Sie keinen eigenen Git Server betreiben, gibt es im Internet naben bitbucket.org und github.com noch viele weitere Anbieter bei denen Sie kostenlos ihren Source Code verwalten und lagern können.)</p>
<br />

![image-title-here](/images/posts/2013-08-29_bitbucket.jpg){:class="img-responsive"}

<br />

<p>Unter "Build Triggers" entscheidet sich, wann der Buildjob ausgeführt werden soll. Wir wählen "Poll SCM" um das zuvor eingerichtete Source Code Management anbinden. Über das Hilfe Menü auf der Rechten Seite lassen sich mehrere nützliche Anwendungszwecke finden, zum Beispiel:</p>
<pre>H/15 * * * *</pre>
<p>Dies prüft unser SCM alle 15 Minuten auf Änderungen. Hat sich an unserem Source Code etwas geändert und wurde diese Änderung in das oben angegebene Git eingecheckt, erkennt dies der Jenkins und startet den Buildprozess.</p>
<br />

<p>Die Kategorien "Configuration Matrix" und "Build Environment" überspringen wir erst einmal und fahren mit "Build" fort.</p>
<p>Fügen Sie hier einen "Invoke Ant" Prozess hinzu</p>

![image-title-here](/images/posts/2013-08-29_invoke_ant.png){:class="img-responsive"}

<br />

<p>Unter 'Post-build Actions' können Sie noch eine 'E-mail Notification' einrichten. So werden Sie immer über den aktuellen Build Zustand informiert.</p>
<h2>InstrumentationTesting mit Jenkins</h2>
<p>Im nächsten Step aktivieren wir unseren Android Emulator. Sollten sie noch keinen bestehenden AVD haben, können sie direkt einen erstellen.</p>

![image-title-here](/images/posts/2013-08-29_buildumgebung.jpg){:class="img-responsive"}

<p>Wird ein Emulator mit Google API benötigt, beispielsweise bei einer Anwendung die Google Maps nutzt, tragen Sie als Android OS Version die benötigte Google API ein.</p>

![image-title-here](/images/posts/2013-08-29_google_api.jpg){:class="img-responsive"}

<br />
<p>Um die Tests zu starten gibt es zwei unterschiedliche Ansätze, zum einen können Sie diese wieder über einen 'Invoke Ant' erstellen:</p>

![image-title-here](/images/posts/2013-08-29_unit_test1.png){:class="img-responsive"}

<p>Die Zweite Möglichkeit dient zum ausführen von sog. Unit Tests. Dabei werden nur einzelne Tests ausgeführt.</p>

![image-title-here](/images/posts/2013-08-29_ant_test.png){:class="img-responsive"}

<p>Anschließend kann der Job gestartet werden um die Tests zu erstellen und startet diese anschließend auf dem Emulator.</p>
<p>In jedem Job lassen sich sog. Trends anzeigen, diese schaffen einen guten Überblick, über alle Vergangenen Tests:</p>

![image-title-here](/images/posts/2013-08-29_jenkins_continuous_test_trend_1.png){:class="img-responsive"}

![image-title-here](/images/posts/2013-08-29_jenkins_continuous_test_trend_2.png){:class="img-responsive"}

<p>Was anfangs noch recht spartanisch aussieht, entwickelt sich nach mehreren tausend durchläufen durchaus zu einer Unübersichtlichen Grafik.</p>
<p>Für diesen Fall hält <a href="https://wiki.jenkins-ci.org/display/JENKINS/reFit+Plugin">das Jenkins Wiki</a> praktische Plugins bereit.</p>

<h3><em>Multikonfigurationsprojekt</em> (Matrix Job)</h3>
<p>Seine wahre Schönheit zeigt das Android Emulator Plugin im sogenannten Matrix Job. Hier haben Sie die Möglichkeit, einen Test auf Unterschiedlichen Emulatoren parallel auszuführen. So lassen Sich Apps beispielsweise in unterschiedlichen Sprachen oder Display Auflösungen ausführen.</p>

![image-title-here](/images/posts/2013-08-29_android_job-variables.png){:class="img-responsive"}

<p>So lassen sich für die Emulator Werte einfach Variablen eintragen, welche für jeden Emulator neu befüllt werden.</p>
<p>In der Job Übersicht werden für jeden Build die Ergebnisse grafisch als Matrix angezeigt.</p>

![image-title-here](/images/posts/2013-08-29_android_matrix-result.png){:class="img-responsive"}
