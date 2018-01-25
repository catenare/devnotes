# Amazon AWS
## Learning Lambda
### AWS Mobile
* Error Message: "error: Uncaught TypeError: Cannot read property 'crypto' of undefined in browser"
    * [Github Issue](https://github.com/aws/aws-sdk-js/issues/1566)
    * [Github Issue Resolution](https://github.com/aws/aws-sdk-js/issues/1512)
    * Resolve: ...culprit is line 4 in rng.ks. In aws-sdk
    * Fixed!! - test: /\.js$/, exclude: /(node_modules)/
