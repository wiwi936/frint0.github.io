---
layout: post
title: Shodan Shenanigans
description: Sex is cool, but have you ever scanned the internet?
url: https://pwnable.club/Shodan-Shenanigans/
image: https://pwnable.club/images/shodan.png
---
<img src="{{ site.baseurl }}/images/shodan.png" alt="Shodan Logo drawn by Pablo Picasso">

I'm sure you've all heard of Shodan. Even the skids and normies have, thanks to HackerGiraffe. It essentially scans the internet for devices
with open ports, and anyone can search through this database. To put it simple, I was bored one afternoon and decided I really needed touch up 
on my android pwning, but where could I possibly find a vulnerable android device for me to viciously and *illegally* take over?
Oh, Shodan exists (Yes, I could throw up an Android VM but thats boring), and so my quest to find a pwnable android begins.

I lazily just go over to shodan and look at the android tag. I see a couple of interesting saved searched but one that caught my attention, 
was **"root shell on android devices"**. Looking at this saved search, I find 60ish devices with port 23 open (telnet). 

<img src="{{ site.baseurl }}/images/search-results.png" alt="Search Results">

At first I really couldn't believe that there was just a telnet shell with root priveleges just waiting for me to log in. 
I log in to the first one (with proxychains) and find myself shocked. Why would port 23 just be open to the public internet, with root priveleges,
ON AN ANDROID, WITH NO AUTHENICATION!!?!? This seemed odd to me. In the proccess of enumeration, I found close to nothing interesting installed.
After taking a screenshot and sending it to my VPS via netcat, the results were odd. This was a smarthome device by a company called **INTERRA** based in Turkey.

<img src="{{ site.baseurl }}/images/interra.png" alt="Screenshot">

Yes, the screenshot was upside down (and i'm leaving it upside down). If you translate the turkish you get something along the lines 
of: 

> "Insert SD Card with INTERRA.apk"


It was as if the device hadn't been setup yet, and telnet was probably left open for debugging purposes. I got bored with this device and went back to shodan in 
search of more rooted android devices with telnet exposed. Anyways, long story short, **ALL** OF THESE ANDROID DEVICES ON SHODAN WERE
THE SAME EXACT SMARTHOME DEVICE! Yes, thats right. Every single one (Just kidding, I only checked 10 but thats enough to convince
me that all of them were the same). Oh and all of them hadn't been setup either. None of them were wifi enabled either so I couldn't find some coordinates
with `wlan_geolocate` on metasploit. This got me thinking, does the telnet service get closed once the device is set up? Now, that wouldn't matter if an attacker
got their payload on the device before hand, and just placed a persistence shell script in init.d. This would leave an attacker with the ability to access
this persons smart home, even after the telnet service is closed. Spooky shit. Anyways, you're probably thinking:

> "Soooo, why'd you even write about this?"

and my answer to that is:

> "Don't buy smart home devices."

Just kidding, but if you're gonna buy a smart home device, just make sure its not from Spain.
