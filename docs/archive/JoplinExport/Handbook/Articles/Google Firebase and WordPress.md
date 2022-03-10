---
title: Google Firebase and WordPress
updated: 2020-09-10 21:43:38Z
created: 2020-09-10 21:43:38Z
---

# Google Firebase and WordPress
Yes, it's technically possible to host a WordPress site on Google Firebase hosting using the WordPress REST API. Google Firebase is a family of services, mostly geared towards mobile development, but includes a very generous hosting allowance for static sites. When building my new personal site, I wanted to build a static site but also have a blog. Looked at some static blog engines but didn't feel like rebuilding the site everytime I create new content. Decided to use WordPress' REST API since I already had a WordPress multi-site running on an Amazon LightSail Server. 
I decided to use Google Firebase hosting because I'm spending a fair amount of time in South Africa and wanted my site to have relative low latency from Johannesburg or New York City. Although Amazon has CloudFront, they don't have any local points of presence in South Africa but Google does. That, plus the cost      (or lack of it), was nice too.
Google also has some nice tools to help with uploading your site on to their system. Using npm, you can install the firebase tools, login to your Google account and you are ready to go. You can configure your service from your command line. 
Other services include both a realtime database and a nosql database. Providing user authentication and running node scripts on their platform is also supported. 
So, I'm using the Amazon API gateway to expose the WordPress REST API to my static sites. The API gateway provides throttling and can also provide caching if necessary. I don't have to worry about my backend server getting overwhelmed by API calls. I can also provide authentication and filtering using the Amazon API gateway.
The front-end for my personal site use Reactjs as the javaScript framework. Now my static site is sitting on a content delivery network and I also get the benefit of having my blog on the same site without the need to have a PHP server running it.