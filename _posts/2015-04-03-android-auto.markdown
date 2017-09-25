---
layout: post
title: "Android Auto"
date: 2015-04-03 12:20:40 +0200
comments: false
categories: [ Programming, Android ]
---
<p>Android Auto was announced on June 25, 2014 at Google I/O in San francisco.
The official mobile App was release on March 19, 2015 for US Accounts only</p>
<p>Since then it has become obvious that google will beat Apple on their Car Play.</p>

{% img /images/posts/2015-04-03_android_auto_main.jpg %}

<p>&nbsp;</p>
<p>At this juncture you can extend your app in two types of representation.</p>
<p>&nbsp;</p>
<h2>Audio Apps</h2>
<p>Here you can browse music and listen to music on android auto</p>
{% img /images/posts/2015-04-03_android_auto_media.jpg %}

<!-- more -->

<h2>Messaging Apps</h2>
<p>recieve incoming notifications, read messages via Text-to-Speak and send replies via voice input</p>
{% img /images/posts/2015-04-03_android_auto_messaging.jpg %}
<p>&nbsp;</p>

<p style="color: #ff0000">Auto-enabled apps cannot be published to Google Play at this time</p>
<p>&nbsp;</p>

<p>I developed an Audio Sample for the Google Developer Group Munich Android Meetup on Aprlil 1, 2015 
in cooperation with Audi Ingolstadt.</p>
{% img /images/posts/2015-04-03_android_auto_unit.jpg %}

<p>Not everyone has access to a Demo System of Android Auto, so Google released an Android Simulator which can be installed right on your phone</p>
<p>These Simulator can be installed via SDK Manager and found at 'android-sdk/extras/google/simulators/'</p>
<p>&nbsp;</p>
<p>Start editing your AndroidManifest, set targetSdk to 21 or higher and add these entry
<pre>&lt;meta-data android:name="com.google.android.gms.car.application"
           android:resource="@xml/automotive_app_desc"/&gt;
</pre>

<p>the resource describe which type of automotive app do you want to offer</p>
<pre>
&lt;automotiveApp&gt;
   &lt;uses name="media"/&gt;
&lt;/automotiveApp&gt;
</pre>

<p>To represent your media on Android Auto, you have to implement an Media Browser.</p>
<p>You will find a complete Sample on github: </p>
<p>https://github.com/googlesamples/android-MediaBrowserService</p>
<p>&nbsp;</p>

<p>Implement the MediaSession.Callback object to enable playback controls</p>
{% codeblock lang:java %}
public void onPlayFromMediaId(String mediaId, Bundle extras)
    //is the callback that the system uses when a MediaItem with the FLAG_PLAYABLE property is clicked

public void onPlay()
    //Invoked if the user chooses play without choosing a specific item

public void onPause() / onStop()
    //do some Magic

public void onSkipToNext() / onSkipToPrevious()
    //skip

public void onPlayFromSearch(String query, Bundle extras)
    //take a deep breath and play some random item
{% endcodeblock %}
</pre>

{% img /images/posts/2015-04-03_android_auto_musicstream.png %}
<p>&nbsp;</p>