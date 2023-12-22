# Walking An Application
---

### Task 1 - Walking An Application
No answer needed

### Task 2 - Exploring the Website
No answer needed

### Task 3 - Viewing The Page Source

First of all, we need to access the IP given.
In my case, 10.10.17.107

Just type it in the browser and hit enter.
This is the page we get:

![Acme IT Support Page](image-1.png)

Task #3 is all about the Page Source.
To access it, all we need to do is right-click anywhere and select "View Page Source" or hit Ctrl + U.

Now on said page, 4 pieces of information stand out. Coincidently (or not), these contain all we need to solve Task #3.

![Page Source of Acme IT Support Page](image-2.png)

In order of appearance, we have:
<ol>
    <li>A comment, before the header, about a new homepage;</li>
    <li>A Few mentions to an "assets" folder;</li>
    <li>An anchor tag pointing us to a "secret-page";</li>
    <li>Another comment, after the footer, about the framework being used, along with its version.</li>
</ol>

Let's solve these one by one:

<b>What is the flag from the HTML comment?</b><br>
If we try to reach the mentioned endpoint, "/new-home-beta", we get the first answer right away.
![First Flag](image-3.png)

<b>What is the flag from the secret link?</b><br> 
Back on the Page Source, we just click on the "/secret-page" anchor tag.
There it is! Our second flag.
![Second Flag](image-4.png)

<b>What is the directory listing flag?</b><br>
The directory listing is probably located in the assets folder.
As we go to <u>10.10.17.107/assets/</u>, we get the following page (with an interesting .txt in it):<br>
![Alt text](image-5.png)<br><br>
Click on the <u>flag.txt</u> and the third flag is found.<br>
![Third Flag](image-6.png)

<b>What is the framework flag?</b><br>
While viewing the Page Source, we notice the page was generated using the "THM" Framework version 1.2.
Furthermore, there's a link pointing us to the framework's webpage: <u>https://static-labs.tryhackme.cloud/sites/thm-web-framework</u>

By accessing the given URL, we land on the following page:
![THM Framework Webpage](image-7.png)

Two important things come to light:
<ol>
    <li>The Acme website is outdated (v1.2);</li>
    <li>A Change Log discussing previous versions.</li>
</ol>

Once we click on the change log, we can see a big issue was solved between versions 1.2 and 1.3: in the former, a directory called "/tmp.zip" kept being created.<br>
![THM Framework Change Log](image-8.png)

This means the Acme IT Support Page probably has the "/tmp.zip" as well.
We access it via our browser and the file is automatically downloaded.<br>

![tmp.zip File](image-9.png)

Open it and, surely enough, there's our fourth flag!<br>

![Fourth Flag](image-10.png)

### Task 4 - Developer Tools - Inspector
As recommended through the task, we now dive into the Acme IT "News" page.

![Acme IT Support Page](image-11.png)

If we attempt to read the 3rd article available, we hit a paywall.

![Article Paywall](image-12.png)

<b>What is the flag behind the paywall?</b>

Let's try to bypass it by inspecting the page (right-click followed by "Inspect" or Ctrl+Shift+I).
During the inspection, we realize the paywall is put up by a div with the name "premium-customer-blocker".

![premium-customer-blocker div](image-13.png)

We can style this div to "display: none".

![display: none](image-14.png)

Voilà! Just like that, the paywall goes away and we get the fifth flag.

![Fifth Flag](image-15.png)

### Task 5 - Developer Tools - Debugger
As pointed out by the task itself, we can see a quick flash of a red rectangle when we click on the "Contact" page.

<b>What is the flag in the red box?</b>

After opening the Inspector Tools and navigating to the Debugger (or Sources, depending on your browser) tab, we notice "flash.min.js".
If we click on it and scroll down, we can see the "flash\['remove']();" function being called.

Let's add a breakpoint on that line by clicking on it.

![Breakpoint](image-16.png)

Refresh the page and we find the red flash!

![Sixth Flag](image-17.png)

### Task 6 - Developer Tools - Network

For our last flag, we'll inspect what's being sent to the server on the Contact page.
For that, we open the Developer Tools and go to the Network tab.

At first, we have these action methods:

![Network Tab](image-18.png)

However, once we type anything into the "Message" textbox and hit "Send Message", a new request appears: contact-msg.

![contact-msg request](image-19.png)

<b>What is the flag shown on the contact-msg network request?</b>

All that's left to do is double-click the "contact-msg" request.
There you go! There's our sixth and last flag!

![Sixth Flag](image-20.png)
