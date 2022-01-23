---
title: general
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# All About APIs - Servers and tools.

## Frameworks
### PHP
* [apigility](https://apigility.org/) - provided by Zend Framework. Swagger support.
* [API Platform](https://api-platform.com/) - REST and GraphQL support.

### Python
* [Falcon](https://falconframework.org/) - Just API framework for Python
* [Django Rest Framework](http://www.django-rest-framework.org/)
* [API Star](https://github.com/encode/apistar)
* [Flask Site](http://flask.pocoo.org)
    * [Frozen Flask](* [Awesome Flask](https://github.com/humiaozuzu/awesome-flask)) - [Site](https://pythonhosted.org/Frozen-Flask/)
        * Used for [Wineries Of the Sierra Foothills](http://www.wineriesofthesierrafoothills.com) and personal site [Johan Martin](http://www.johan-martin.com)
        * Generate static site from flask site.
    * [Awesome Flask](https://github.com/humiaozuzu/awesome-flask)

### Node.js API Frameworks
* [Loopback](https://loopback.io/)
* [Strapi](https://strapi.io/)
* [Restify](http://restify.com/)
* [Koa](http://koajs.com/)

## API Tools
### Docs
* [API Central Docs](https://devdocs.io/)
### API Documentation Tools
* [RAML](http://raml.org/)
* [Swagger](http://swagger.io/)
### API Mock Tools
* [MockServer](https://www.mock-server.com) - Has Docker config
* [WireMock](https://github.com/tomakehurst/wiremock) - Java
* [Osprey Mock Service](https://github.com/mulesoft-labs/osprey-mock-service) - RAML mock service. 1.0 compatible.
* [Osprey Service](https://github.com/mulesoft/osprey)
* [Prism](http://stoplight.io/platform/prism/) - run locally
* [Swagger-codegen](https://github.com/swagger-api/swagger-codegen) - Has Docker Config
* [Imposter](https://github.com/outofcoffee/imposter) - Has Docker config

### Mock Service
* [Mockbin](http://mockbin.com/) - test, mock and track http requests & responses

### How To - Mock API Server
* [Mock Rest API with JSON Server](https://coligo.io/create-mock-rest-api-with-json-server/) - Create your own mock API server with faker.js
* [Testing External APIs with Mock Servers](https://realpython.com/blog/python/testing-third-party-apis-with-mock-servers/) - Use python for testing
* [Go Raml](https://github.com/Jumpscale/go-raml)

## Other
* [Standalone RAML API Mocking Tools Surface](https://www.programmableweb.com/news/standalone-raml-api-mocking-tools-surface/2015/08/13) - Article - Mock tools
* [RAML and Osprey - a Better Way to Build Mock APIs](https://www.tcias.co.uk/blog/2015/03/11/raml-and-osprey-a-better-way-to-build-mock-apis/)
* [Sandbox](https://getsandbox.com/) - online service for API mocking

### Creating a mock api server - node.js
* Using `json-server`
* Setup
    1. Create directory - *test_server*
    1. `touch server.js` - server startup file
    1. `npm init` - create config file. Set `server.js` as the start script.
    1. Create `server.js` file.
    1. `npm install faker json-server --save-dev`

```json
    //server.js
    const jsonServer = require('json-server')
    const customers = require('./customers')
    const server = jsonServer.create()
    const router = jsonServer.router(customers())
    const middlewares = jsonServer.defaults()

    server.use(middlewares)
    server.use(router)
    server.listen(3000, () => {
      console.log('JSON Server is running')
    })

    //customer.js
    var faker = require('faker')
    function generateCustomers () {
        var customers = []
        for (var id = 0; id < 50; id++) {

        var firstName = faker.name.firstName();
        var lastName = faker.name.lastName();
        var phoneNumber = faker.phone.phoneNumberFormat();

        customers.push({
            "id": id,
            "first_name": firstName,
            "last_name": lastName,
            "phone": phoneNumber
        })
    }
    return { "customers": customers}
    }
    module.exports = generateCustomers
```

## REST Test Endpoints
* [JsonPlaceHolder](https://jsonplaceholder.typicode.com/)
* [Random User Generator](https://randomuser.me/)

# Projects of interest

## Software Engineering
* Kevlin Henney - #KevlinHenney

## Web
### Tools to watch
* [Vapor](http://vapor.codes/) - Swift3 framework for web application development.
* [Electrode](http://www.electrode.io/index.html) - made by Walmart. ReactJS framework essentially.

### JavaScript
* [elm](http://elm-lang.org/)
    * [Tutorial](https://guide.elm-lang.org/)
    * [Awesome list of Elm Tutorials](https://github.com/isRuslan/awesome-elm)
* [GrapeJs](http://grapesjs.com/) - Web builder framework. JavaScript. Sites without coding. Integrate into own site.
* [Monaco Editor](https://github.com/Microsoft/monaco-editor) - Microsoft javascript based code editor.


## Resource Lists
* [Awesome Awesome List](https://github.com/bayandin/awesome-awesomeness) - List of lists
* [Awesome Weekly](https://awesomeweekly.co/) - [Github](https://github.com/sindresorhus/awesome)
* [Awesome Serverless List](https://github.com/travist/awesome-serverless-1)
* [Awesome Python](https://awesome-python.com/)
* [Awesome Boilerplates & Templates](https://github.com/melvin0008/awesome-projects-boilerplates)
* [Awesome Elm Tutorials](https://github.com/isRuslan/awesome-elm)
* [Awesome Flask](https://github.com/humiaozuzu/awesome-flask)
* [Awesome PHP](https://github.com/ziadoz/awesome-php)
* [Awesome Angular](https://github.com/AngularClass/awesome-angular)
* [Awesome Angular Components](https://github.com/brillout/awesome-angular-components)
* [Awesome IOS](https://github.com/vsouza/awesome-ios) - [main site](http://awesomeios.com/)
* [Awesome Kotlin](https://github.com/KotlinBy/awesome-kotlin)
* [Front-end Dev Bookmarks](https://github.com/dypsilon/frontend-dev-bookmarks)
* [raywenderlich.com](https://www.raywenderlich.com) - IOS/development resources
### List of lists
* [Sindresourhus](https://github.com/sindresorhus/awesome)
* [Useful and silly lists](https://github.com/jnv/lists)

## Algorithm Resources
* [Grokking Algorithms Source](https://github.com/egonSchiele/grokking_algorithms)
* [Elementary Algorithms and Data Structures](https://github.com/liuxinyu95/AlgoXY)
* [The Coders Hub](https://github.com/thecodershub/algorithms) - Algorithms in multiple languages

## Other
* [Boomerang](http://www.seas.upenn.edu/~harmony/) - Data conversion and synchronization
* [Unison](https://www.cis.upenn.edu/~bcpierce/unison/) - File sync utility

* Report Servers
    * [ReportServer](https://reportserver.net/en/) - integrates Birt reports. Open Source

## Serverless
* [Serverless](https://github.com/serverless/serverless) - serverless framework

## Mobile Prototyping Tools
* [Marvel](https://marvelapp.com/features/) - Prototyping tool
* [CSS3 Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations) - use for interactivity
* [Hammer](http://hammerjs.github.io/) - JavaScript library for touch.
* [Axure](https://www.axure.com/#a=features) - Has a free educational version.

## Other Projects
* [freeCodeCamp](https://github.com/freeCodeCamp)
    * [Mail For Good](https://github.com/freeCodeCamp/mail-for-good) - Open Source email campaign management tool.
    * [Conference For Good](https://github.com/freeCodeCamp/conference-for-good)
* [what 3 words](https://support.what3words.com/hc/en-us) - location alternative to addresses
* [Apostrophe CMS](http://apostrophecms.org/) - Node.js based CMS

## Event Management Software
* [Attendize](https://www.attendize.com) - self-hosted ticket sales online (think EventBrite)
* [Open Source Event Manager](https://github.com/openSUSE/osem) - Ruby on Rails event manager for tech conference
* [Open Conference Ware](https://github.com/osbridge/openconferenceware) - Ruby on Rails conference manager.
* [Event Espresso](https://github.com/eventespresso/event-espresso-core) - Wordpress Plugin

## RPC Framework
* [gRPC](https://grpc.io/)
* [Apache Thrift](https://thrift.apache.org/)

## Service Providers
* [Church Insight](http://www.churchinsight.com/) - church admin software.
* [Pilot](https://pilot.com/) - bookkeeping software.

## Asset Management
* [Cloudinary](https://cloudinary.com/) - Digital Asset Management in the cloud. Has a free tier.
    * Has a wordpress plugin
* [Filestack](https://www.filestack.com/) - Has a free tier.

## Edge Services
* [Fastly](https://www.fastly.com/) - CDN/Edge servers.

## Other Services
* [Sentry](https://docs.sentry.io/learn/context/) - has a free tier.
    * Error tracking service. Able to rack from JavaScript, PHP, Java, Python.
* [FormSpree](https://formspree.io/) - Form to email. First 1000 are free.

## Animation
* [GSAP](https://greensock.com/gsap)


## Presentation Frameworks [Web based]
* [Impress](https://github.com/impress/impress.js)
* [Remark](https://github.com/gnab/remark)
* [Deck](https://github.com/imakewebthings/deck.js)
* [WebSlides](https://github.com/webslides/WebSlides)

## Lists for marketing site
* [Places To Post Your Startup](https://github.com/mmccaff/PlacesToPostYourStartup)

## Blockchain
* [Non-financial Blockchain](https://github.com/machinomy/awesome-non-financial-blockchain)

## Free Services for Devs
* [Free for Devs](https://github.com/ripienaar/free-for-dev)
