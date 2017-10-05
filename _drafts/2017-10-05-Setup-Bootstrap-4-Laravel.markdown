---
layout:     post
title:      "Setting up Bootstrap 4 in Laravel 5.5"
subtitle:   "How to correctly configure Bootstrap 4 in Laravel 5.5"
date:       2017-10-05 12:00:00
author:     "Dylan"
header-img: "img/bootstrap-laravel.jpg"
category: dev
tags: [laravel, bootstrap, config]
---


<h2 class="section-heading">Background</h2>

<p>I have a number of projects in the workings and one of them is using the Laravel PHP framework. In this post I will show you how to update your bootstrap version to the latest (Bootstrap 4 Beta at the time of writing). Bootstrap has been very useful to me over the past couple years. I have used Bootstrap 3 extensively for various companies I have worked for. Therefore as Bootstrap 4 is now in beta I thought I would pull it in to my current project.</p>

<h2 class="section-heading">Dive in!</h2>

<p>For the purposes of this guide I will go from installing a brand new Laravel project and then make the necessary adjustments. The same can be done on an existing project.</p>

Create a new Laravel project called blog
{% highlight shell %}
~$ laravel new blog
{% endhighlight %}

<img src="{{ site.baseurl }}/img/installLaravel.png" alt="Laravel Installing...">
<span class="caption text-muted">Creating Laravel Application</span>

<p>
Once that completes, if you Valet and you have added the directory to Valet's paths you will be able to visit http://blog.dev and you should have the Laravel index page displayed in the browser.
</p>

<p><strong>Remove</strong> Bootstrap 3 Sass Library</p>
{% highlight shell %}
~/blog$ npm uninstall bootstrap-sass --save-dev
{% endhighlight %}

<p> I use the --save-dev flag so that the library is removed from the package.json file. </p>
<p> Bootstrap 4 depends on JQuery and also the Popper.js library. Laravel has already included JQuery. So all we need to do is pull in Bootstrap 4 and Popper.js. We will do that now...</p>

{% highlight shell %}
~/blog$ npm install bootstrap@4.0.0-beta --save-dev
{% endhighlight %}
<p>After installing you should get a warning from NPM showing you that there are dependencies that are not installed yet. <strong>Important! We do not need to save a new JQuery dependency to our package.json file.</strong> Laravel has this setup for us already.</p>

<p>Install the Popper.js library</p>
{% highlight shell %}
~/blog$ npm install popper.js@^1.11.0 --save-dev
{% endhighlight %}

<p>Now we can run npm install to fetch everything according to the package.json file. What this will do is pull in JQuery and also the other dependencies. </p>

{% highlight shell %}
~/blog$ npm install
{% endhighlight %}

<p>At this point we installed all the necessary libraries and files, we just need to refer to the correctly now. To start off with we will edit the bootstrap.js file found in the ~/blog/resources/assets/js/</p>
