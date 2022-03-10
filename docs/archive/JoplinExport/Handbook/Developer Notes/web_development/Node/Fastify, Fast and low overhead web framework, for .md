---
title: Fastify, Fast and low overhead web framework, for Node.js
updated: 2021-04-06 10:00:04Z
created: 2021-04-06 10:00:04Z
source: https://www.fastify.io/
---

[<img width="91" height="28" src="../../../../_resources/fastify-logo-menu.d13f8da7a965c8_69c85f34c67e4068a.png"/>](https://www.fastify.io/)

[Home](https://www.fastify.io/) [Docs](https://www.fastify.io/docs/latest) [Ecosystem](https://www.fastify.io/ecosystem) [Benchmarks](https://www.fastify.io/benchmarks) [Contribute](https://www.fastify.io/contribute) [Blog](https://medium.com/@fastifyjs/) [Help](https://github.com/fastify/help)

[GitHub](https://github.com/fastify/fastify) [Twitter](https://twitter.com/fastifyjs)

# <img width="320" height="98" src="../../../../_resources/fastify-logo-inverted.2180cc6b19_2cb925a5a46948709.png"/>

## Fast and low overhead web framework, for Node.js

# Why

An efficient server implies a lower cost of the infrastructure, a better responsiveness under load and happy users. How can you efficiently handle the resources of your server, knowing that you are serving the highest number of requests possible, without sacrificing security validations and handy development?

Enter Fastify. Fastify is a web framework highly focused on providing the best developer experience with the least overhead and a powerful plugin architecture. It is inspired by Hapi and Express and as far as we know, it is one of the fastest web frameworks in town.

# Who is using Fastify?

Fastify is proudly powering a large ecosystem of organisations and products out there.

Discover [more organisations using Fastify](https://www.fastify.io/organisations). Do you want your organisation to [be featured here](https://www.fastify.io/organisations#how-to-be-featured)?

- [![Mr Porter is using Fastify](../../../../_resources/mrp.366c52cf20c7664b_237a527f743a4bc7ab16e3d9e866f.svg)](https://www.mrporter.com)
- [<img width="152" height="60" src="../../../../_resources/habit.bddfda611001c895_dc5ab53ffaf44c24a6bf5648b62.svg"/>](https://habit.global/)
- [<img width="133" height="60" src="../../../../_resources/logdna.68fb856ea6333916_8e0b17a4ed704e5da2db5ff71c.svg"/>](https://logdna.com)
- [<img width="60" height="60" src="../../../../_resources/swissdev-javascript-jobs-200-200_794d50c324cc4ce59.svg"/>](https://swissdevjobs.ch/)
- [<img width="281" height="60" src="../../../../_resources/microsoft.8f028edbe9fe9d40_13e91f6eb5514036be272ee.svg"/>](https://docs.microsoft.com)
- [<img width="148" height="60" src="../../../../_resources/quero-educacao.30fc7cc391afc572_587f6cb373264a4ba6.svg"/>](https://sobre.quero.com/)
- [![Seznam.cz is using Fastify](../../../../_resources/seznam.0e852b48d7670e1e.cz_084d41afe7c14f65852f4f9.svg)](https://www.seznam.cz/)
- [![Radity is using Fastify](../../../../_resources/radity.4eee1d7016ba6062_85e29bcf1be54a1a8fb003d98e.svg)](https://www.radity.com)
- [<img width="85" height="60" src="../../../../_resources/global-cto-forum.5a4e391465f443b_a28a5caba3af4bbc8.svg"/>](https://www.globalctoforum.org)
- [<img width="190" height="60" src="../../../../_resources/fabfitfun.7aa398cf7d47c48a_45af47ce0d6647e1a11a616.svg"/>](https://fabfitfun.com/)
- [![Satiurn is using Fastify](../../../../_resources/satiurn.1a5149cc66d4dc6d_9ddda710cd5146259d46c8517.svg)](https://www.satiurn.com/)
- [<img width="245" height="60" src="../../../../_resources/nucleode.fc9b4dd4588c1716_4eabfabd4057493e89ceed68.svg"/>](https://www.nucleode.com)

# Core features

These are the main features and principles on which fastify has been built:

- **Highly performant:** as far as we know, Fastify is one of the fastest web frameworks in town, depending on the code complexity we can serve up to 30 thousand requests per second.
- **Extendible:** Fastify is fully extensible via its hooks, plugins and decorators.
- **Schema based:** even if it is not mandatory we recommend to use [JSON Schema](https://json-schema.org/) to validate your routes and serialize your outputs, internally Fastify compiles the schema in a highly performant function.
- **Logging:** logs are extremely important but are costly; we chose the best logger to almost remove this cost, [Pino](https://github.com/pinojs/pino)!
- **Developer friendly:** the framework is built to be very expressive and to help developers in their daily use, without sacrificing performance and security.
- **TypeScript ready:** we work hard to maintain a [TypeScript](https://www.typescriptlang.org/) type declaration file so we can support the growing TypeScript community.

# Quick start

Get fastify with NPM:

```
npm install fastify
```

Then create `server.js` and add the following content:

async/await

```
// Require the framework and instantiate it
const fastify = require('fastify')({ logger: true })

// Declare a route
fastify.get('/', async (request, reply) => {
  return { hello: 'world' }
})

// Run the server!
const start = async () => {
  try {
    await fastify.listen(3000)
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start() 
```

Finally, launch the server with:

```
node server
```

and you can test it with:

```
curl http://localhost:3000
```

## Request/Response validation and hooks

Of course, Fastify can do much more than this.

For example, you can easily provide input and output validation using JSON Schema and perform specific operations before the handler is executed:

async/await

```
const fastify = require('fastify')({ logger: true })

fastify.route({
  method: 'GET',
  url: '/',
  schema: {
    // request needs to have a querystring with a `name` parameter
    querystring: {
      name: { type: 'string' }
    },
    // the response needs to be an object with an `hello` property of type 'string'
    response: {
      200: {
        type: 'object',
        properties: {
          hello: { type: 'string' }
        }
      }
    }
  },
  // this function is executed for every request before the handler is executed
  preHandler: async (request, reply) => {
    // E.g. check authentication
  },
  handler: async (request, reply) => {
    return { hello: 'world' }
  }
})

const start = async () => {
  try {
    await fastify.listen(3000)
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()
```

## TypeScript Support

Fastify is shipped with a typings file, but you may need to install `@types/node`, depending on the Node.js version you are using.

The following example creates a http server.

We pass the relevant typings for our http version used.

By passing types we get correctly typed access to the underlying http objects in routes.

If using http2 we'd pass `<http2.Http2Server, http2.Http2ServerRequest, http2.Http2ServerResponse>`.

For https pass `http2.Http2SecureServer` or `http.SecureServer` instead of Server.

This ensures within the server handler we also get `http.ServerResponse` with correct typings on `reply.res`.

async/await

```
import Fastify, { FastifyInstance, RouteShorthandOptions } from 'fastify'
import { Server, IncomingMessage, ServerResponse } from 'http'

const server: FastifyInstance = Fastify({})

const opts: RouteShorthandOptions = {
  schema: {
    response: {
      200: {
        type: 'object',
        properties: {
          pong: {
            type: 'string'
          }
        }
      }
    }
  }
}

server.get('/ping', opts, async (request, reply) => {
  return { pong: 'it worked!' }
})

const start = async () => {
  try {
    await server.listen(3000)

    const address = server.server.address()
    const port = typeof address === 'string' ? address : address?.port

  } catch (err) {
    server.log.error(err)
    process.exit(1)
  }
}
start()
```

Visit the [Documentation](https://www.fastify.io/docs) to learn more about all the features that Fastify has to offer.

# A fast web framework

Leveraging our experience with Node.js performance, Fastify has been built from the ground up to be **as fast as possible**. Have a look at our [benchmarks section](https://www.fastify.io/benchmarks) to compare fastify performance to other common web frameworks.

[Checkout our benchmarks](https://www.fastify.io/benchmarks)

# Ecosystem

Fastify has an ever-growing ecosystem of plugins. Probably there is already a plugin for your favourite database or template language. Have a look at the [Ecosystem page](https://www.fastify.io/ecosystem) to navigate through the currently available plugins. Can't you find the plugin you are looking for? No problem, [it's very easy to write one](https://www.fastify.io/docs/master/Plugins)!

[Explore 179 plugins](https://www.fastify.io/ecosystem)

# The team

In alphabetical order

## Lead Maintainers

<img width="96" height="96" src="../../../../_resources/52195_v_4_s_460_39b9a5ad26c745b28b9086ad5f6caca1.jpg"/>

Matteo Collina

<img width="96" height="96" src="../../../../_resources/4865608_v_4_s_460_f8ef97c96096422aac564143ca3665ae.jpg"/>

Tomas Della Vedova

## Collaborators

<img width="96" height="96" src="../../../../_resources/1054125_v_4_s_460_ffcee18b4bb9448987c8f6bdc01de09f.jpg"/>

Tommaso Allevi

<img width="96" height="96" src="../../../../_resources/16144158_s_460_v_4_b9a6bfdf8d5142b28931bb155f877a8.jpg"/>

Ethan Arrowood

<img width="96" height="96" src="../../../../_resources/11050534_s_460_v_4_5cad32c4890c40afbe4b9a0f6ed9885.jpg"/>

Ayoub El Khattabi

<img width="96" height="96" src="../../../../_resources/1297759_v_4_s_460_692d40e092834c69a8108b4975637fce.jpg"/>

Cemre Mengu

<img width="96" height="96" src="../../../../_resources/1190716_s_460_v_4_23e96542751a45279b711cc90588a7d3.jpg"/>

David Clements

<img width="96" height="96" src="../../../../_resources/1764424_v_4_s_460_4b824a9e89de441e8a0ec56c43a0dc75.jpg"/>

Dustin Deus

<img width="96" height="96" src="../../../../_resources/26234614_v_4_s_400_43c7c664056648679733c292c78a17e.jpg"/>

Rafael Gonzaga

<img width="96" height="96" src="../../../../_resources/6959636_s_460_v_4_036282c03e334ca5958cf248f33bc1dd.jpg"/>

Vincent Le Goff

<img width="96" height="96" src="../../../../_resources/205629_v_4_s_460_93648036804340f39f95c95cc811f3c1.jpg"/>

Luciano Mammino

<img width="96" height="96" src="../../../../_resources/2510597_s_460_v_4_331a7c563a154357a67fe76d8a85eeb7.png"/>

Salman Mitha

<img width="96" height="96" src="../../../../_resources/1847934_s_460_v_4_ef3c9901773c4fbdb2ac20e4c576714f.jpg"/>

Igor Savin

<img width="96" height="96" src="../../../../_resources/1303687_v_4_s_400_1eb063b5b0d34667b487ca84061518ee.jpg"/>

Evan Shortiss

<img width="96" height="96" src="../../../../_resources/1620916_s_460_v_4_ef9ef64fc6e140b99da300bb87ff9779.jpg"/>

Maksim Sinik

<img width="96" height="96" src="../../../../_resources/43814140_s_460_v_4_f75fb515720f4601a1622158d88d020.jpg"/>

Frazer Smith

<img width="96" height="96" src="../../../../_resources/11404065_s_460_v_4_97d3ccd1d1ef471885f41aca6831509.jpg"/>

Manuel Spigolon

<img width="96" height="96" src="../../../../_resources/321201_v_4_s_460_9fbddb6161ef49ffab6a7c2fa80a9c09.png"/>

James Sumners

<img width="96" height="96" src="../../../../_resources/5128013_v_4_s_460_8e8ced4281074b8daccaee7fc7094266.jpg"/>

Nathan Woltman

## Past Collaborators

<img width="96" height="96" src="../../../../_resources/16024985_s_400_v_4_0abbd0789e0340edaf035f249ee5ad6.jpg"/>

Trivikram Kamat

<img width="96" height="96" src="../../../../_resources/9213230_v_4_s_460_f6dc983289d345b9bc044bf1c4f35aa8.jpg"/>

Çağatay Çalı

# Acknowledgments

This project is kindly **sponsored by**:

- [NearForm](http://nearform.com)
- [Microsoft](https://opensource.microsoft.com/)

Past Sponsors:

- [LetzDoIt](http://www.letzdoitapp.com)

Also thanks to:

- [The amazing Fastify community](https://github.com/fastify/fastify/graphs/contributors)

# Hosted by

We are currently an incubated project at the [OpenJS Foundation](https://openjsf.org/).

[<img width="380" height="119" src="../../../../_resources/openjsf-knockout.2e1aee2e40559fa_bf572e615f5d4f22b.svg"/>](https://openjsf.org/)

*Found a typo or want to improve this page?* [Submit a PR on GitHub](https://github.com/fastify/website/blob/master/src/website/layouts/home.html)

Fastify, Copyright © 2016-2021 [OpenJS Foundation](https://openjsf.org/) and [The Fastify team](https://github.com/fastify/fastify#team), Licensed under [MIT](https://github.com/fastify/fastify/blob/master/LICENSE)

Icons by simpleicons.org