# Developer Helper Tools
## Server Mock Tools
* [MailCatcher](https://mailcatcher.me/) - Localhost email intercept
* [Ngrok](https://ngrok.com/) - Secure tunnel to localhost

## API Tools
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


### How To - Mock API Server
* [Mock Rest API with JSON Server](https://coligo.io/create-mock-rest-api-with-json-server/) - Create your own mock API server with faker.js
* [Testing External APIs with Mock Servers](https://realpython.com/blog/python/testing-third-party-apis-with-mock-servers/) - Use python for testing
* [Go Raml](https://github.com/Jumpscale/go-raml)

### Other
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

### Miscellaneous Notes
* [Boomerang](http://www.seas.upenn.edu/~harmony/)
* [Unison](https://www.cis.upenn.edu/~bcpierce/unison/) - File sync utility