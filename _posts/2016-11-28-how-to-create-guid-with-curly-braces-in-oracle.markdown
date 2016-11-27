---
layout: post
title: How to create guid with curly braces in oracle
categories: Oracle
excerpt: Here is creation of guid with curly braces with oracle
---

Here is creation of guid with curly braces with oracle

{% highlight sql %}
create or replace package COMMON
as
  FUNCTION NEW_ID RETURN VARCHAR2;
end;
	/
	
create or replace package body COMMON
as
  FUNCTION NEW_ID RETURN VARCHAR2
  AS
    tmpRetVal VARCHAR2(100);
    tmpId RAW(16);
  BEGIN
    SELECT SYS_GUID() INTO tmpId FROM DUAL;
    tmpRetVal := '{'
     //SUBSTR(tmpId, 0, 8)
                //'-'
                //SUBSTR(tmpId, 8, 4)
                //'-'
                //SUBSTR(tmpId, 12, 4)
                //'-'
                //SUBSTR(tmpId, 16, 4)
                //'-'
                //SUBSTR(tmpId, 20, 13)
                //'}';
                
    DBMS_OUTPUT.PUT_LINE('Original: '//tmpId//CHR(13)//'Formatted: '//tmpRetVal);
                
    RETURN tmpRetVal;            
  END;
end;
/

{% endhighlight %}

Example usage:
{% highlight sql %}
	SELECT COMMON.NEW_ID FROM DUAL;
{% endhighlight %}

Output:

{% highlight sql %}
	{2D71F811-19F6-F4AC-C985-3DA501193F548}
{% endhighlight %}