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


## Notes
* [Multiple View Instances on Same Page](https://codingexplained.com/coding/front-end/vue-js/using-multiple-vue-instances-page)

## Wordpress
* [Wordpress API](../../../php/wordpress/api/vuejs.md) - notes for Wordpress API

## Tutorials
* [Vue Abstract Components](https://alligator.io/vuejs/vue-abstract-components/)
* [Vue Lazy Load Images](https://alligator.io/vuejs/vue-lazy-load-images/)

## Components
* [Vue The Mask](https://github.com/vuejs-tips/vue-the-mask/blob/master/src/docs/docs.vue)
* [Vue Cookie Law](https://github.com/apertureless/vue-cookie-law)
* [Vue Class Component](https://github.com/vuejs/vue-class-component)
* [Vee Validate](https://github.com/baianat/vee-validate)
    * Clear all errors and make fields pristine:
        * `this.field = ""`
        * `this.$validator.reset()`

## Importing vue components - *script.ts* - *template.html*
```html
<div class="grid-container">
    <h1>{{msg}}</h1>
    <marvel-proto></marvel-proto>
</div>
```
* *script.ts*
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

## Creating new project with vue-cli
* Setup the proxy
* In *vue.config.js*
```json
  devServer: {
    proxy: 'http://localhost:5000'
  }
```
* Setup typescript
    * `npm install -D @vue/cli-plugin-typescript`
    * `vue invoke typescript`
