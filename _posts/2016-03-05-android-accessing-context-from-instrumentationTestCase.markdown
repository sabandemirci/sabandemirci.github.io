---
layout: post
title: Accessing context.getFilesDir() from InstrumentationTestCase
categories: Android
excerpt: In order to fix getting null value problem while using Context.getFilesDir() inside InstrumentationTestCase,you need to create `files` directorory.
---

In order to fix getting null value problem while using Context.getFilesDir() inside InstrumentationTestCase,you need to create `files` directorory.

{% highlight shell %}
adb shell
cd /data/data/package_id_of_app
mkdir files
{% endhighlight %}

Now following test assertion codes will  not fail.

{% highlight java %}
assertNotNull(getInstrumentation().getContext().getFilesDir());
assertNotNull(getInstrumentation().getContext().openFileInput("aa.db"));
{% endhighlight %}