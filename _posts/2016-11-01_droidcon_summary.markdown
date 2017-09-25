---
layout: post
title: "Droidcon UK Summary"
date: 2016-11-01 19:52:03 +0200
comments: false
sharing: false
categories: Android
---
<p>Like every year, I had again the pleasure again of attending Droidcon UK in London last week.
I'd like to share my impressions with you all. The following is a quick summary of some speeches I attended.</p>

<h2>Keynote</h2>
<br />
<p>Google's Chief Game Designer Noah Falstein spoke about how development has evolved over the years.
He started as a game designer in 1980s and worked on popular games like Sinistar, Secret of Monkey Island and
Indiana Jones. In the keynote he demonstrated a relationship between cave-paintings and VR. 
He also gave a prospective about future VR and AR and explained his cause of why VR is much more than just a gaming technology.</p>

<!-- more -->

<h2>Did you test it?</h2>
<p>The first speech I attended, was an overview on testing without a dedicated QA team.
Derek Rozycki and Kirk Chambers gave some recommendations on how to create good test plans and state diagrams.
They reminded every attendee to think outside the happy path while testing an app.
Also a good tip was to check if deep links could create shortcuts for your test, when the app state isn't important for the testcase itself.</p>
<br />

<h2>Get Ready for Android Wear 2.0</h2>
<p>The Googlers Hoi Lam and Agnieszka Madurska explored the past and presented the future of Android Wear.
They gave an insight of the Android Wear team and how they created the WearableRecyclerView.
A significant introduction was a wear emulator for round wearables with a flat.</p>
<br />

<h2>Android Testing Support Library</h2>
<p>Zan Markan explored the various stages of the Android Testing Support Library. 
He discovered test Rules, rest Runners and how to bring out the maximum of Expresso and Firebase's Cloud Test Lab.
A useful implementation of 'scrollableScrollTo' for espresso tests was open sourced on github</p>
<br />
<a href="https://github.com/zmarkan/Android-Espresso-ScrollableScroll">https://github.com/zmarkan/Android-Espresso-ScrollableScroll</a>
<br />


<h2>Lightening Talks #1</h2>
<h3>Infer</h3>
<p>Facebook's engineer Martino Luca started the lightening talks with a summary of Infer, the static code analysis tool from facebook.
Completely integrated in Android studio and the gradle build process, the tool should decrease the amount of faults in every app.</p>
<br />


<h3>Optimising the performance of VectorDrawable</h3>
<p>My GDG Collegue Florina Muntenescu from Berlin gave some tips how to improve performance when using vector drawables.
Replacing all PNGs with vector drawables can shrink the APK but then results in a slower app performance.
The talk gave a nice insight on how vector drawables are rendered and when you should avoid using them.</p>
<br />


<h3>7 Ways to improve your Gradle build</h3>
<p>Tania Pinheiro explores 7 simple ways to improve android gradle builds. </p>
<ul>
<li>use extra properties for version numbers eg. support library</li>
<li>use manifest-placeholders to replace strings or resources in the manifest</li>
<li>use custom scripts </li>
<li>change the default build type for test-runs eg. run tests always against a mock</li>
<li>extract singing credentials to a separate properties file (increase security)</li>
</ul>
<br />

<h3>Flat as a Pancake</h2>
<p>The two Facebook engineers Emil Sjörlander and Pasquale Anatriello gave a funny talk about nested and boring layouts.
Flattening the view hierarchy isn't enough. They shared measurements and tricks to increase the layout performance with
a newly created tool from Facebook where every developer can create performant apps.</p>
<br />
<a href="https://code.facebook.com/posts/531104390396423/components-for-android-a-declarative-framework-for-efficient-uis/">Declarative android framework</a>
<br />


<h2>Moshi</h2>
<p>Serj Lotutovici talked about the pros and cons of Moshi a modern json library.
In his talk he gave some numbers and comparison to Jackson and Gson</p>
<br />
<a href="https://github.com/square/moshi">https://github.com/square/moshi</a>
<br />


Keeping it Clean</h2>
<p>
Rich King a Senior Developer at Badoo talked about his pains when changing architectures.
While they messed around with many different approaches, they created a complete chat framework for Android
which is opensourced on github. </p>
<br />
<a href="https://github.com/badoo/Chateau/">https://github.com/badoo/Chateau/</a>
<br />


<h2>Android Architecture Blueprints</h2>
<p>David González and Jose Alcérreca explored their motivations to create a sample project to create a discussion basis
for architectures. 
This collection was created by the community and curated by Google and become an official Google sample.
It contains samples for loaders, databinding, clean code and as well dagger and rxjava implementations.</p>
<br />
<a href="https://github.com/googlesamples/android-architecture">https://github.com/googlesamples/android-architecture</a>