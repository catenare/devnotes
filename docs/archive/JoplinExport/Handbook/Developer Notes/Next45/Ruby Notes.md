---
title: Ruby Notes
updated: 2021-07-03 16:09:49Z
created: 2021-07-03 16:09:18Z
latitude: -26.16670000
longitude: 27.86670000
altitude: 0.0000
tags:
  - add-platform
  - bundle
  - gemfile
  - heroku
---

* Issue: An app’s Gemfile.lock that is generated with Bundler 2.2.3 locally may not work on Heroku unless the Linux platform is explicitly “locked”:
* `bundle lock --add-platform x86_64-linux`