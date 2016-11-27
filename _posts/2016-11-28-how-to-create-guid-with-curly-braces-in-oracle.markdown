---
layout: post
title: How to create guid with curly braces in oracle
categories: Oracle
excerpt: Here is creation of guid with curly braces with oracle
---

Here is creation of guid with curly braces with oracle

{% highlight sql %}
create or replace package GUID_GENERATOR
as
  FUNCTION CREATE_GUID RETURN VARCHAR2;
end;
/	
create or replace package body CREATE_GUID
as
  FUNCTION CREATE_GUID RETURN VARCHAR2
  AS
    tmpRetVal VARCHAR2(100);
    tmpId RAW(16);
  BEGIN
    SELECT SYS_GUID() INTO tmpId FROM DUAL;
    tmpRetVal := '{' 
          ||SUBSTR(tmpId, 0, 8)
          ||'-'
          ||SUBSTR(tmpId, 8, 4)
          ||'-'
          ||SUBSTR(tmpId, 12, 4)
          ||'-'
          ||SUBSTR(tmpId, 16, 4)
          ||'-'
          ||SUBSTR(tmpId, 20, 13)
          ||'}';
                
    RETURN tmpRetVal;            
  END;
end;

{% endhighlight %}

Example usage:
{% highlight sql %}
	SELECT GUID_GENERATOR.CREATE_GUID FROM DUAL;
{% endhighlight %}

Output:

{% highlight sql %}
	{4250F57F-FB03-213C-AE05-34132A8C01BA3}
{% endhighlight %}