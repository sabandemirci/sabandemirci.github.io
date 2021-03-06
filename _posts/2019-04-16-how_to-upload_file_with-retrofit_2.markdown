---
layout: post
title: How to upload file with retrofit 2
categories: Android
excerpt: For uploading files to server with `Retrofit 2` here is two way to manage with.
published: true
---

For uploading files to server with `Retrofit 2` using octet-stream content type


**Web Service**
{% highlight java %}
@POST
@Path("/uploadFile")
@Consumes(MediaType.APPLICATION_OCTET_STREAM)
public Response uploadFile(@Context HttpServletRequest request,InputStream fileInputStream) {
{% endhighlight %}

**Android**

{% highlight java %}
@POST("uploadFile")
@Headers( {"Content-Type: application/octet-stream"})
Call<JsonObject> uploadFile(@Body RequestBody fileInputStream);
{% endhighlight %}

**Usage**

{% highlight java %}
File file = new File(document.getPath());
byte[] byteArray = IOUtils.toByteArray(new FileInputStream(file));
RequestBody requestBody = RequestBody.create(MediaType.parse("application/octet-stream"), byteArray);
Response<JsonObject> answer = restClient.getService().uploadFile(requestBody).execute();
if (answer.isSuccessful()) {
    
}
{% endhighlight %}