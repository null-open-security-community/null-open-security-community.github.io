---
layout: post
title: Web threats ..a new wave! – by Hemanshu
---

Today omnipresence of internet makes your browser the favorite attack vector for bad guys. Initially content filtering solutions (think websense) looked effective in curbing malicious website, but of recent there has been a new revival in the malicious websites and what is interesting is more and more legitimate websites are getting infected(msn canda , nitie ,Bank-of-India). Once a legitimate site starts distributing malware or is compromised there is little your web filtering solution or firewall could do about it. To add to injury attackers have now turned to obfuscate the attack payload to evade any security apparatus like IPS in place. Javascript looks like to be the tool of choice; its universally supported in all browsers (and in pdfs too..but that’s again a long story). Known attacks like Gumbler have started leveraging obfuscation an excellent description is here. These obfuscations make it very hard for signature based security engine to confidently detect and attack.

<!--more-->

I have never been a fan of signature matching solutions, they are dumb and reactive and would always do more false positive than a DPI based solution. Robert Graham does a nice analysis here .

And things are only gonna get more interesting from here. Think of a payload which do a Javascript ? VbScript ? Javascript transformation. JavaScript are just the beginning, browsers are becoming the next platforms, with every universal plugin will brings newer threats with it ( Java Applets, Flash, third party plugin).

The need of the hour is to develop more heuristic and context aware engines. Solving this problem at the network is gonna be a challenge , instead of perimeter; proxy could be a more suitable carrier (as latency is only to the web requests, in case of IPS the latency is added to the whole network). but nothing could do it faster than a end point solution (And please I am not talking the stupid Anti Virus!)
