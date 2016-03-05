---
layout: post
title:  "Accessing context.getFilesDir() from InstrumentationTestCase"
date:   2016-03-05 12:34:00 +0000
categories: android
---
In order to fix getting null value problem while using Context.getFilesDir() inside InstrumentationTestCase,you need to create `files` directorory.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

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
