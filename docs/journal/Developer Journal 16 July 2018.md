# Developer Journal 16 July 2018
## Monday 16 July 2018
* Need to finish form for my nziswano site.
    * Web components for my form
        * Captcha
        * Submit form
        * Validation
            * Not empty
            * Email address
        * URL for submitting to captcha form on AWS
    * Create form
* Income
    * Work on sending out some requests.
    * Maybe go see Sean and help him with some stuff.
    * Need to get some clients for my digital domain
        * Digital agencies
* Work on lookfindme.com - trying to finish up the site.
    * Create lookfindme.com with static first 2 pages.
    * HTML web components.
* Web component for the form
    * Building a web component
        * [What are web components](https://www.webcomponents.org/introduction#what-are-web-components-)
    * Creating my first component
        * 
    * Goal: Submit form to my aws account
        * Review johan-martin.com
        * Header - x-api-key: - create api key for this form.
            * Send this key to api gateway.
    - [ ] x-api-key - key from aws api gateway
    - [ ] captcha url - url to submit data.
        - [ ] Email to send information to - form destination
```js
baseUrl = "https://api.paseo.org.za/johan/";
captchaKey = "captchaKey";
formDestination = "martin.johan@johan-martin.com";
formUrl = "https://gateway.johan-martin.com/addform";
x-api-key = key from aws api gateway
data = {
captcha: capchaKey,
destination: formDestination 
}
headers['x-api-key']
url = formUrl
ajax call - headers, data, url, post
```

* Notes - git (version control)
    * Branch based
        * Slows the flow of information between the developers
        * Integration credit card - pay the debt off somehow.
    * Trunk based development
        * Fewer merge conflicts
        * Code review - smaller chunks
        * Feature flags - keep features away until ready from consumers.
        * Don't have to worry about debt.
        * Pull requests
            * Code reviews
    * Github flow
        * Continuous deployment
        * Use metrics to check for problems
        * Every pull request gets deployed to production
        * Tasks
            * Lock master
            * Merge master into deploy
            * Build and test
            * deploy to canary
            * deploy to production
            * merge into master - unlock master
        * Issue: Scale - get stuck in deploy queue - lock master
    * Decorators - declarative programming in JavaScript
### Web Components - learn about them
* Resources
    * [Web Components.org - What are web components](https://www.webcomponents.org/introduction#specifications)
    * [W3c Web Components - GitHub](https://github.com/w3c/webcomponents/)
    * [Google Web Fundamentals](https://developers.google.com/web/fundamentals/web-components/)
* Web Component Tutorial
    * Using [webpack](https://webpack.js.org/concepts/) 
    * [babel-loader](https://github.com/babel/babel-loader)
    * [TypeScript](https://www.typescriptlang.org/index.html)
        * [TypeScript with Babel](https://github.com/Microsoft/TypeScript-Babel-Starter#readme)
        * `tsc --init --declaration --allowSyntheticDefaultImports --target esnext --outDir lib`
        * [awsome-typescript-loader](https://github.com/s-panferov/awesome-typescript-loader)
## Tuesday 17 July 2018
* Web components - trying to get a basic environment set up.
* Finished with setting up form on nziswano site. Using jQuery. Just need to get it done so I can work on the lookfindme site.
* Need to see Sean to help him with some stuff.
## Wednesday 18 July 2018
* Finally applied for some positions. Hope to get something out of it. We'll see. Will have to do more. Need to finish up my sites.
* Need to work on the lookfindme site.
* Already got the first rejection.
    * Need to work on a proposal/opening for flickr - maybe they need some WordPress developers. Can't hurt to ask.
## Thursday 19 July 2018
* Talked to Offerzen about getting listed on their platform. Need to update my profile.
* First working on getting at least stripe working for tonight.
## Friday 20 July 2018
* Waiting to hear back from offerzen.
* User
    * first
    * last
    * location
    * email
    * industry
* JobSeeker
  * company: string = "";
  * first: string = "";
  * last: string = "";
  * name: string = "";
  * telephone: string = "";
  * location: string = "";
  * email: string = "";
  * industry: string = "";
  * about: string = "";
  * photo: string = "";
  * isAvailable: boolean = true;
  * availability: string = "";
  * employmentTypes: string[] = [];
  * experience: string = "";
  * industries: string[] = [];
  * positions: string[] = [];
* Build tools
* Vuetify
    * Demo file
    * `browser-sync start --server --watch`
* NPM
    * 5 items
    * `npx browser-sync`
    * `npm outdated`
    * `npm upgrade`
    * `npm start`
    * `npm run`
* Stripe
    * `payment testing`
    * Vuejs Integration - [Elements Vue Integration](https://alligator.io/vuejs/stripe-elements-vue-integration/)
    * Trying with - [Elements QuickStart](https://stripe.com/docs/stripe-js/elements/quickstart)
    * Add script to index.html - `<script src="https://js.stripe.com/v3/"></script>`
    * Create Creating r