# Vuejs Notes

## Resources
* [Vue](https://vuejs.org/) - main site
* [Vue-loader](https://vue-loader.vuejs.org/en/) - Using Vue with Webpack
* [Vue Foundation](https://github.com/vue-foundation/vue-foundation) - template for using Foundation with Vue and Webpack
* [Vue Font Awesome](https://github.com/Justineo/vue-awesome)
* [Vue Admin](https://github.com/vue-bulma/vue-admin)
* [Vuex](https://github.com/vuejs/vuex)
* [Vuex Rest API](https://github.com/christianmalek/vuex-rest-api)
### Replacement resources
* [axios](https://github.com/mzabriskie/axios) - Replacement for vue resources http
    * [How to use axios as your http client](http://codeheaven.io/how-to-use-axios-as-your-http-client/) - Section on setting headers in Axios.
    * [Axios with Vue](https://alligator.io/vuejs/rest-api-axios/) - Use in component

## Setup with Webpack
* [Configuration Information](configuration.md)

## Notes
* [Multiple View Instances on Same Page](https://codingexplained.com/coding/front-end/vue-js/using-multiple-vue-instances-page)

## Wordpress
* [Wordpress API](../../../php/wordpress/api/vuejs.md) - notes for Wordpress API

## Tutorials
* [Vue Abstract Components](https://alligator.io/vuejs/vue-abstract-components/)
* [Vue Lazy Load Images](https://alligator.io/vuejs/vue-lazy-load-images/)

## Importing vue components - *script.ts*
```js
import MarvelProto from './../MarvelProto/MarvelProto.vue'
export default {
    components: {
        MarvelProto,
    },
    data: () => (
        {
            msg: "User List",
        }
    ),
};
```
