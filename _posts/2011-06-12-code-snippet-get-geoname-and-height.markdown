---
layout: post
title: Geoname and height from Lat/Long
date: 2011-06-12 16:37:44 +0200
comments: false
sharing: false
categories: Links
---
With this little Code Snippet, it is possible to get the Height and Geonames of the current Region.

Example:

{% highlight java %}
try {
    URL url = new URL( "http://ws.geonames.org/srtm3?lat=" + tfBreitenGrad.getText() + "&amp;lng=" + tfLaengenGrad.getText() );
    URLConnection connection = url.openConnection();
    BufferedReader br = new BufferedReader( new InputStreamReader(connection.getInputStream() ));
    String erg = br.readLine(); // hier kommt die höhe rein
    tfErgHoehe.setText(erg); // hier setz ich die höhe im fenster bzw bei dir dann in der anwendung
} catch (IOException e1) {
    e1.printStackTrace();
}
{% endhighlight %}