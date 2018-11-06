---
layout: post
title: "Android Gradle"
date: 2015-02-21 14:09:19 +0200
comments: true
categories: [ Programming, Android ]
---
<p>Gradleware released Gradle 2.3 this week, so I decided to write my overdue 
post about Gradle and the new Android buildsystem for Android Studio.</p>
<p>Google announced the new Gradle-based build system on Mai 15, 2013 at Google I/O in San francisco.</p>
<p>&nbsp;</p>

![image-title-here](/posts/2015-02-21_gradle_android_logo.png %}
<p>&nbsp;</p>


"Gradle is first of all an open-source build system general purpose platform agnostic with extensions for java, c++, scala, android, et cetera"
Hans Dockter https://gradle.org/hans-dockter founder of Gradleware

<p>what are the benefiz of gradle to make it worth, switching from maven or ant</p>
+ performance
+ maintainability
+ usability
+ extendability
+ standardazitaion
<p>&nbsp;</p>

<p>A Famous quote has nothing to do with software development but you can apply it</p>

"We make the impossible possible, the possible easy, and the easy elegant."
Moshé Feldenkrais

<p>Gradleware, the company behind Gradle, want to apply those requirements in gradle</p>
<p>&nbsp;</p>

<!-- more -->

<h1>Basics of Groovy and Gradle</h1>
<p>Groovy runs inside the Java Virtual Machine and makes use of Java's libraries.</p>

"Groovy is Java with an additional jar file as dependency, Groovy in Action"
Dierk Konig

<p>&nbsp;</p>
<p>Groovy reuses Java semantics and API, but removes a lot of syntax noise eg. semicolons</p>
<p>So every Groovy type is a subtype of java.lang.Object and every object is an instance of
a type in the normal way.</p>
<p>&nbsp;</p>

<p>Syntax alignment</p>
<pre>
import java.util.*;         // Java
Date today = new Date();    // Java

today = new Date()          // Groovy

require 'date'              # Ruby
today = Date.new            # Ruby
</pre>

{% highlight java %}
apply plugin: "java"
description = "This is my description"

repositories {
  mavenCentral()
}

dependencies {
  compile "org.springframework:spring-core:4.0.5.RELEASE"
}

test {
  jvmArgs "-Xmx1024m"
}
{% endhighlight %}

<h2>Gradle build scripts</h2>
+ written in a Groovy-based DSL
+ Tasks and plugins can be written in Groovy
+ named build.gradle by default
+ doesn't run in groovy runtime

<h2>Tasks</h2>
<p>Running 'gradle tasks' gives you a list of the main tasks of the selected project</p>
<p>add '-b' or '--build-file' for customized script name eg. 'gradle -b test.gradle tasks'</p>
{% highlight groovy %}
task sampleTask {
    doFirst {
        println "doFirst"
    }

    doLast {
        println "doLast"
    }
}
{% endhighlight %}

<p>All Tasks implement the org.gradle.api.Task interface.</p>
<p>You can find all methods on the official documentation:</p>
http://gradle.org/docs/current/dsl/org.gradle.api.Task.html#N16B7D