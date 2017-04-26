---
layout: post
title: World’s slimmest TCP port scanner – By @
---

Ok, the name is a pun on Titan’s watch 😛 and is something that is an outcome of a really cool bash feature which I’ll be discussing. Bash provides a way to create a TCP connection or send UDP packets to a host on  a given port, the cool thing is that you don’t have to rely on other scripting languages or programs for creating sockets/network connections when writing a shell script. Using this feature one can write simple to complex network utilities/scripts (a sigh of relief for scriptters :-) if that is that a word ).
NOTE: This is a bash provided feature(if it is compiled with –enable-net-redirections option) and has nothing to do with /dev Devices.

Using these sockets/connections is as simple as accessing a file which is inline with the unix philosophy. All you need to do is to read/write to files of the form:

/dev/<protocol>/<host>/<port>

where, <protocol> = tcp | udp
<host> = hostname | IP
<port> = port number.

For example, lets say you want to send a custom payload to a web server, you can do it with the following command:

$echo -en “HEAD / HTTP/1.0\r\n\r\n”  > /dev/tcp/example.com/80

You won’t get anything in return for obvious reasons(no read!). Now you’ll say what good can this be. Well, you can assign it a fd and read and write to that fd if your script is a network interactive one and expects some data in response.

Example commands:
# 15 is just random fd that I chose, you can choose any fd number you like.

$exec 15<> /dev/tcp/example.com/80
$echo -en “HEAD / HTTP/1.1\r\nhost: example.com\r\n\r\n” >&15
$cat <&15
HTTP/1.1 302 Found
Date: Thu, 30 Jul 2009 21:56:37 GMT
Server: Apache
Location: https://example.com:443/
Connection: close
Content-Type: text/html; charset=iso-8859-1

Finally, time for the slimmest TCP port scanner:

#!/bin/sh
# Usage:>$tcpscan.sh <host> <start_port> <end_port>

for p in `seq $2 $3`;do  (echo “foo” > /dev/tcp/$1/$p) &> /dev/null ; RET=$?; if [ $RET -eq 0 ]; then echo “$p/tcp open”; fi; done

I know it looks ugly :-P, no sanity checks etc, had to keep it slim you know…
Tell me when u use it in your shell scripts.
