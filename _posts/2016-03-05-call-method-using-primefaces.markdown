---
layout: post
title: How to call managed bean' s method using Primefaces
categories: Java
excerpt: In order to fix getting null value problem while using Context.getFilesDir() inside InstrumentationTestCase,you need to create files directorory.
---

Hello everyone, If you would like to call managed bean' s method from javascript, Primefaces p:remoteCommand is exactly what you are looking for.

{% highlight html %}
<p:remoteCommand name="myCustomFunction" actionListener="#{bean.method}" />
{% endhighlight %}

this command generate following javascript code:

{% highlight html %}
<p:commandLink id="commandLink" actionListener="#{bean.method}" onclick="myCustomFunction"/>
{% endhighlight %}