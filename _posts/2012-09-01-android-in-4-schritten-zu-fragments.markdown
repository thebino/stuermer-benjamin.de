---
layout: post
title: "Android – In 4 Schritten zu Fragments"
date: 2012-09-01 23:06:32 +0200
comments: false
sharing: false
categories: 
---

Mit Einführung von Android 4.0 hat Google die Phone Layouts mit den Tablet Layouts wieder vereint. Um den Entwicklern eine Möglichkeit zu bieten, eine App sowohl für Phone als auch Tablet zu erstellen, wurden sog. Fragments eingeführt.
<br /><br />
Mit Ihnen ist es möglich, zwei Activities in einem Tablet Layout bsp. nebeneinander zu verwenden.
<br /><br />

1) Erstellen des Fragment Layouts

[/res/layout/text_fragment.xml] 
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<TextView
xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="fill_parent"
android:layout_height="wrap_content"
android:text="@string/text"
/>
{% endhighlight %}

<!-- more -->


2) Fragment Class erstellen

[/src/your.package/TextFragment.java]
{% highlight java %}
import android.support.v4.app.Fragment;
import android.view.LayoutInflater;
 
public class TextFragment extends Fragment {
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.text_fragment, container, false);
    }
}
{% endhighlight %}

3) Fragment in ursprungs Layout einfügen

[/res/layout/main.xml]
{% highlight xml %}
<fragment
    android:id="@+id/news_fragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    class="de.stuermerbenjamin.exampleview.TextFragment" />
 {% endhighlight %}

4) MainActivity Class anpassen

{% highlight java %}
public class ExampleViewActivity extends Activity {
{% endhighlight %}
ändern in:
{% highlight java %}
public class ExampleViewActivity extends FragmentActivity {
{% endhighlight %}
 
Nun verwendet ihre Anwendung Fragments ;D