---
layout:     post
title:      "Token Authentication with Vue and Laravel (Part 1)"
subtitle:   "Users, Permissions and Roles using Token Based Authentication"
date:       2017-10-20 12:00:00
author:     "Dylan"
header-img: ""
category: dev
tags: [laravel, VueJS, Authentication]
---

<h2 class="section-heading">Let dive right in...</h2>

<p>Today I will be sharing about my experience on putting together token based authentication for a single page application (SPA). The technologies used are Laravel and VueJS. Initially I was googling quite a bit however right in the Laravel documentation the explanation is sufficient. To achieve our task we will need to do the following:</p>

- Install Laravel
- Install Laravel Passport
- Clean up JS and laravel boilerplate code so that we have a true single page application (SPA)
- Install Vue, Vue-Router and Vuex
- Serverside Role and Permission setup for users
- Configure token issuing from the server using Laravel Passport

Please note this is a multi-part post. I will link the rest of the series below
