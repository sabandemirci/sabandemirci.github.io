---
layout: post
title: Hpw to upload file with retrofit 2
categories: Android
excerpt: >-
  For uploading files to server with `Retrofit 2` here is two way to manage
  with.
published: true
---

For uploading files to server with `Retrofit 2` here is two way to manage with.
**Solution**

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
