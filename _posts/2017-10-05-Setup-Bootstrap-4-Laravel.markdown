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

<p>I have a number of projects in the workings and one of them is using the Laravel PHP framework. In this post I will show you how to update your Bootstrap version to the latest (<a href="https://getbootstrap.com/">Bootstrap 4 Beta</a> at the time of writing). Bootstrap has been very useful to me over the past couple years. I have used Bootstrap 3 extensively for various companies I have worked for. Therefore as Bootstrap 4 is now in beta I thought I would pull it in to my current project.</p>
<br>
<p>Assumptions - You are able to run a <a href="https://laravel.com/">Laravel</a> project on your computer and just need to update to the next Bootstrap version.</p>

<h2 class="section-heading">Dive in!</h2>

<p>For the purposes of this guide I will go from installing a brand new Laravel project and then make the necessary adjustments. The same can be done on an existing project.</p>

Create a new Laravel project called blog
{% highlight shell %}
~$ laravel new blog
{% endhighlight %}

<img src="{{ site.baseurl }}/img/installLaravel.png" alt="Laravel Installing...">
<span class="caption text-muted">Creating Laravel Application</span>

<p>
Once that completes, if you have <a href="https://laravel.com/docs/5.5/valet">Valet</a> installed and you have added the directory to Valet's paths you will be able to visit http://blog.dev and you should have the Laravel index page displayed in the browser.
</p>

<h2 class="section-heading">Manage NPM dependencies</h2>
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



<h2 class="section-heading">Update references in code</h2>
<p>At this point we have installed all the necessary libraries and files, we just need to refer to them correctly now. To start off with we will edit the bootstrap.js file found in the ~/blog/resources/assets/js/ folder. All we need to do is update the require to say "bootstrap" instead of "bootstrap-sass". For clarity I have left the old one commented out so you can see what needs to be removed. </p>
{% highlight javascript %}
try {
    window.$ = window.jQuery = require('jquery');

    //require('bootstrap-sass'); <-- Remove this line
    require('bootstrap');

} catch (e) {}
{% endhighlight %}

<p>Next we need to import the correct files in our app.scss. Currently its trying to import the old Bootstrap 3 files. Lets do that now... Open up the app.scss file found in the ~/blog/resources/assets/sass/ folder. Change it to look like the following :</p>

{% highlight scss %}


@import url("https://fonts.googleapis.com/css?family=Raleway:300,400,600");

@import "variables";

@import "~bootstrap/scss/bootstrap";

{% endhighlight %}

<h2 class="section-heading">Finally manage SASS overrides</h2>
<p>In version 4 Bootstrap have moved from using pixels (px) internally to using rem units. See the blog post <a href="http://blog.getbootstrap.com/2017/08/10/bootstrap-4-beta/">here</a> where one of the points explain the move. What this means for us is that our SASS overrides need to use the same units when it comes to font sizes etcetera. Laravel has some standard overrides already included in the project. To enable our project to run correctly we need to change just one. We need to update $font-size-base to use rem units. We will do this now. </p>

<p>Open up the _variables.scss file located in the ~/blog/resources/assets/sass/ folder and make the following adjustments </p>

{% highlight scss %}

// Body

$body-bg: #f5f8fa;

// Borders

$laravel-border-color: darken($body-bg, 10%);
$list-group-border: $laravel-border-color;
$navbar-default-border: $laravel-border-color;
$panel-default-border: $laravel-border-color;
$panel-inner-border: $laravel-border-color;

// Brands

$brand-primary: #3097D1;
$brand-info: #8eb4cb;
$brand-success: #2ab27b;
$brand-warning: #cbb956;
$brand-danger: #bf5329;

// Typography

//$icon-font-path: "~bootstrap-sass/assets/fonts/bootstrap/"; <-- Remove

$font-family-sans-serif: "Raleway", sans-serif;
$font-size-base: 1rem; // <-- Important Change

$line-height-base: 1.6;
$text-color: #636b6f;

// Navbar

$navbar-default-bg: #fff;

// Buttons

$btn-default-color: $text-color;

// Inputs

$input-border: lighten($text-color, 40%);
$input-border-focus: lighten($brand-primary, 25%);
$input-color-placeholder: lighten($text-color, 30%);

// Panels

$panel-default-heading-bg: #fff;

{% endhighlight %}
<span class="caption text-muted">Two changes under the Typography section</span>

<p>The icon-font-path is no longer relevant as Bootstrap no longer ships with Glyphicons. There are <a href="https://getbootstrap.com/docs/4.0/extend/icons/">suggestions</a> on the Bootstrap documents to guide you in this respect. For now we don't need to worry about the font path so we can remove it. </p>

<h2 class="section-heading">Success!</h2>
<p>This setup completes the necessary steps to run Bootstrap 4 with Laravel 5.5. When working with the Frontend on Laravel you can compile down your SASS and JS with the following NPM commands:</p>

{% highlight shell %}
~/blog$ npm run dev
{% endhighlight %}

<p>Alternately you could run the watcher: </p>

{% highlight shell %}
~/blog$ npm run watch
{% endhighlight %}

<br>

<p> I hope this post has helped you get on your way developing your next big idea with Laravel and Bootstrap 4. Please <a href="/contact">contact</a> me and let me know what you thought of this post. Or connect via social media below in the footer.</p>
