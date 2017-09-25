---
layout: post
title: "Horizontaler Activity Wechsel in Android"
date: 2012-07-14 22:59:46 +0200
comments: false
sharing: false
categories: Android
---
Neben den Gestures gibt es noch eine zweite Lösung, um

mit “seitlichem wischen” zwischen Activities zu wechseln.

Die Rede ist vom ViewPager.


Bekannt wurde dieser mit dem Wechsel des Android Markets
zu Google Play sowie der überarbeiteten Google+ App.

{% img left /images/posts/2012-07-14_ViewPager.jpg %}
<!-- more -->

Verwendet werden können die ViewPager bereits ab der
Android Version 1.6
Hierzu müssen dem Projekt die Compatibility Library hinzugefügt werden.

Wichtig ist, bei der Verwendung im Layout, dass man den
kompletten Klasennamen verwendet:


{% codeblock lang:java %}
&lt;android.support.v4.view.ViewPager  android:layout_width="match_parent"  android:layout_height="match_parent"  /&gt;
{% endcodeblock %}
Bitte beachten: layout_height="wrap_content" funktioniert NICHT beim ViewPager