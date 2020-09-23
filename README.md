<div align="center">

## Fix for ASP \.NET Web Forms acting 'buggy' after user presses 'back' button


</div>

### Description

If you do ASP.NET web forms, have you noticed that they seem to act buggy after the user hits the back button? For example, do events start firing off that shouldn't be, or does the state on the form get reset to what the user typed in 2 times ago, or worse?

It's not a bug...and here's how to fix it.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Ian Ippolito \(vWorker\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/ian-ippolito-vworker.md)
**Level**          |Beginner
**User Rating**    |5.0 (15 globes from 3 users)
**Compatibility**  |VB\.NET, ASP\.NET
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__10-9.md)
**World**          |[\.Net \(C\#, VB\.net\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/net-c-vb-net.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/ian-ippolito-vworker-fix-for-asp-net-web-forms-acting-buggy-after-user-presses-back-button__10-160/archive/master.zip)





### Source Code

I ran into this problem
while creating a website that had a _change event coded.  It worked fine
the first time through, but whenever the user hit the back button, the _change
event would fire even though the user hadn't changed anything.</font></span></p>
<p><span lang="en-us"><font size="2">    I discovered the problem
was NOT a bug.  Instead it is caused by a peculiar interaction between the
ASP.NET view state mechanism (which allows pages to 'remember' your control
states) and the browser's cache, which in my case was IE 6.0.<br>
<br>
    Basically, the browser overrode the HTML rendered by
ASP.NET's view state mechanism with its cached contents.  This might be
fine on old style ASP pages, but with ASP.NET web forms, the fact that the cache
'remembered' the new setting of my control, forced the _change event to fire,
even though the user hadn't selected it after hitting back.</font></span></p>
<p><span lang="en-us"><font size="2">    Once you understand the
problem, the fix is simple, just disable the browser's caching as the first line
in your Page Load.  You should do this for all ASP.NET form pages that have
event handling.  Turning off caching won't affect performance, because
these type of pages load dynamically every time, anyway.</font></span></p>
<p><span lang="en-us"><font size="2">   Hope this saves you some
headaches!</font></span><BR>
<BR>
<b><font face="Courier New" size="2">Response.Cache.SetExpires(Now())
<br>
Response.Cache.SetCacheability(HttpCacheability.NoCache)</b><BR>

