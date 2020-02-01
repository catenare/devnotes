# Paseo Baptist Church Template

- Based on Foundation
- Using `foundation-cli` and `foundation starter template`

## Goal:

1. Keep in sync with starter template while creating custom sites.
1. Used by Wordpress as it's template.

- Use as a static page with Wordpress API to provide content.
  - Allow use of AWS CDN - faster access to the page since wordpress will be hosted on AWS.
  - Easier to build pages in Foundation with Panini.

## Customizations

1. Added `font-awesome` to the mix
1. Changed server port to **8888** and disable automatic opening of browser.

## Notes:

1. Site hosted on Amazon VPS service.
1. Code on github

## Partials Used

## Webpack - We're using vue as a component and webpacker to manage it.

- Vue component is included via git
- Using babel with gulp, hence the gulp.babel.js
- Not tied to wordpress currently.
- Webpack seems to be working just fine with gulp. Something investigate more in the future, especially if building commponents rather than SPAs.

* Need to find a replacement for panini.
