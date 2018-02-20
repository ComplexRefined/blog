---
layout:     post
title:      "Issues with Valet"
subtitle:   "Sorting out your Valet installation"
date:       2018-02-14 12:00:00
author:     "Dylan"
header-img: "img/tools.jpg"
category: setup
tags: [valet, laravel, environment, tools]
---

<h2 class="section-heading"> Background </h2>
<p>A short while ago, I came up against a really simple issue. My Laravel Valet was not working. I say simple because in the end it was very easy to fix however trying to work out what had happened was a small nightmare.</p>

<p>I started a project some time back with Laravel 5.3. And since then I have obviously upgraded twice to Laravel 5.5. Having said that I will need to upgrade to 5.6 soon. Anyway the reason I am telling you this is because at the time I started the project I also installed <a href="https://laravel.com/docs/5.5/valet">Laravel Valet</a> as my tool of choice to get my web server up and running. The ease with which you can serve and share sites was very attractive to me.</p>

<h2 class="section-heading"> First Problem</h2>
<h5>.dev tld has been registered by Google</h5>
<p>Finding some time to work on my project I opened it up and navigated to my project on Chrome and found that the project could not be found.</p>
<img src="{{ site.baseurl }}/img/siteUnreachable.png" alt="Site Unreachable Image">


<blockquote>...easily fixed I thought</blockquote>
<p>I did some reading and found that the .dev tld has been registered by Google and therefore Chrome flat out refuses to load my project from a localhost. Easily fixed I thought, so I updated Valet and Dnsmasq and made sure Valet was serving sites on the *.test tld. Lots of people had experienced the same issues (see https://github.com/laravel/valet/issues/431)</p>

<p>To my surprise I was still having the same issue. Looking around the web I found lots of people having similar issues.</p>
<h5> I tried the following: </h5>
<ul>
  <li>Reinstalled Brew</li>
  <li>Updated dependencies in Brew</li>
  <li>Uninstalled and reinstalled Valet</li>
  <li>Uninstalled and reinstalled PHP (Upgraded to 7.2)</li>
  <li>Uninstalled and reinstalled Dnsmasq. Plenty of people solved their issues by doing this and then also resetting Valet to serve under the *.test tld. I however was not that lucky.</li>
</ul>

<h2 class="section-heading">Second Problem</h2>
<h5>Something else is going on</h5>
<p>Based on the fact that a lot of the solutions pointed to the fact that Dnsmasq was not working correctly I started looking at what files and configurations Dnsmasq relied upon. And this is where I found my error...</p>
<br>
<p>Almost immediately I found the error. <strong>The Dnsmasq.conf file!!</strong> </p>
<p>On my installation the file was located at \usr\local\etc\dnsmasq.conf. When I inspected the file I found the error immediately. Right at the bottom of the dnsmasq.conf file when Valet is installed, it comes with its own dnsmasq.conf file. So at the end of the file you can configure further options for Dnsmasq. Valet utilises this and points Dnsmasq to wherever your valet installation is. (By default this is /Users/{username}/.valet/dnsmasq.conf).</p>
<blockquote>I learned that I had installed Valet for different user accounts on my Mac!</blockquote>

<p>So when looking at the paths at the bottom of my \usr\local\etc\dnsmasq.conf file, I noticed that there were <strong>two</strong> paths pointing to <strong>two</strong> different Valet installations. I learned that I had installed Valet under 2 different user accounts.</p>
<img src="{{site.baseurl}}/img/twoPaths.png" alt="Two paths in dnsmasq.conf file">

<h2 class="section-heading">The fix</h2>
<p>I removed the incorrect path and left the correct path to my Valet installation. Thereafter I typed "valet restart".</p>
<p>I then visited my project under the *.test tld and I saw the correct webpage served.</p>
<br>

<p>I hope that this was helpful if you were trouble shooting as I was. I intend on posting more about my day to day development soon.</p>
