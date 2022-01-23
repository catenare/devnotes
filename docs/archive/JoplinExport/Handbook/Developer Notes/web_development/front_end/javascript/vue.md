---
title: vue
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Working with Vue in Foundation
* Used foundation-cli to install foundation
## Setup
* Install vue, vue-loader, vue-style-loader, vue-template-compiler, sass-loader, style-loader, css-loader, typescript, awesome-typescript-loader
### *gulpfile.babel.js* config
* Configure *gulpfile.babel.js - webpack*
* `gulp.watch('src/assets/components/**/*').on('all', gulp.series(javascript, browser.reload))` - add to end of file to watch components
```js
let webpackConfig = {
  resolve: {
    extensions: ['.ts', '.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        use: [
          {
            loader: 'babel-loader'
          }
        ]
      },
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: {
          loaders: {
            scss: ['vue-style-loader', {
              loader: 'css-loader',
              options: {
                minimize: false,
                sourceMap: false
              }
            },
              {
                loader: 'sass-loader',
                options:
                  {
                    includePaths: ['./src/assets/vue/styles'],
                    data: '@import "./src/assets/vue/styles/app";',
                    sourceMap: false
                  }
              }
            ],
            ts: 'awesome-typescript-loader'
          }
        }
      },
      {
        test: /\.ts$/,
        loader: 'awesome-typescript-loader'
      },
      {
        test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        loader: 'url-loader',
        query: {
          limit: 10000,
          name: 'fonts/[name].[hash:7].[ext]'
        }
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: [
          'file-loader?name=images/[name].[ext]'
        ]
      }
    ]
  }
}
```
* Have to configure webpackConfig with vue-loader.
* Update *config.yml*
```yaml
  assets:
    - "src/assets/**/*"
    - "!src/assets/{components,img,js,scss,fonts}/**/*"
```
### Other Notes
* Created separate style directory for just Vue styles.
    * Allow access to foundation from all components.
    * Easier configuration in webpack.
* Installed *babel-preset-env* for always current babel engine.
* Customize the *app.css* file in *./src/assets/vue/styles*
    * *@import '~foundation-sites/scss/foundation';*
    * ~~*@import '~font-awesome/scss/font-awesome';*~~ - Not necessary since already in main config.
    * *@import '~motion-ui/src/motion-ui';*


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


# General notes while developing with Vue

## Updated Resources
* Vue filters no longer included.
    * [vue2-filters](https://github.com/freearhey/vue2-filters) - Restore vue1 filters
* Use methods on *v-for* rather than filter. Call the item as a method
* Ex:
    * `<li v-for=" story in famous(stories) " >`
```js
    methods: {
        famous: (stories) => {
            return stories.filter(  (item) => {

                console.log(item)

                return item.upvotes > 20
            })
        },
        now: function () {
           return Date.now()
        }
    },
```
* Ajax requests for Vue
* [axios](https://github.com/mzabriskie/axios) - Replacement for vue resources http

## TypeScript Notes
* [Vue Typescript](https://vuejs.org/v2/guide/typescript.html)
* [vue-class-component](https://github.com/vuejs/vue-class-component)
* `npm install vue-class-component` - Component annotations for Vue.

```js
// tsconfig.json
{
  "compilerOptions": {
    // ... other options omitted
    "allowSyntheticDefaultImports": true,
    "lib": [
      "dom",
      "es5",
      "es2015.promise"
    ],
    "module": "es2015",
    "moduleResolution": "node"
  }
}
```
## Vue Components
* [Unknown Custom Element Error](https://forum-archive.vuejs.org/topic/2036/component-inside-component-unknown-custom-element-error-vueify/4)
* Include component globally
```js
import Hello from '../vue/components/Hello'
Vue.component('hello', Hello)
```
    * Now available globally

* Include component locally
* [Getting elements in vue with vanilla javascript](https://forum.vuejs.org/t/getting-elements-in-vue-with-vanilla-javascript/8668/2)
    * this.$el.querySelector('p')

## Child/Parent Communication
* How to get the parent to update it's value from the child.
* Vuejs 2 changed how it is done. .sync has changed.
* Components
    * Parent - wordpress
    * Child - story
        * props: [story, favorite]
* On Child
    * button - `<button v-show="!isFavorite" @click="setFavorite" class="success button tiny">Favorite</button>` - on click, call setFavorite method.
    * method - emit event to favorite, send the current story as the object.
```js
    private setFavorite() {
        this.$emit("favorite", this.story);
    }
```
* On Parent
    * in Template - `v-on:favorite="updateFavorite(story)` - event is favorite, method is updateFavorite and pass in the story.
```html
    <story v-for="story in stories"
            :key="story.id"
            :story="story"
            :favorite="favorite"
    v-on:favorite="updateFavorite(story)"></story>
```
* method to update the favorite the current story.
```js
    public updateFavorite(story) {
        this.favorite = story;
    }
```
* Favorite is now pointing to the current story. Only one favorite.

## Create module for npm
* [Vue Component Publish to npm](https://vuejsdevelopers.com/2017/07/31/vue-component-publish-npm/)

## VueRouter
* Getting Router hooks to work in vue-class-component.
    * [VueClassComponent Readme](https://github.com/vuejs/vue-class-component) - Adding Custom Huooks
* Fix issue with relative css files not being loaded. Cause page not to reload.
    * Added base reference.
    * [Base Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base)
    * Can also add it in router module.
        * [Route Options](https://router.vuejs.org/en/api/options.html#routes)
* Fix Issue with TypeScript and router.push - Argument type `{name: string} is not assignable to parameter RawLocation.
    * [Missing TS Definitions](https://github.com/vuejs/vue-router/issues/1312)
    * Not yet in package - [Fix](https://github.com/druppy/vue-router/blob/25267faee57571510f3e7b04d0939c4ff69ca180/types/router.d.ts)

## Vuex
* Using mapGetter in vue-class-component
    * [Vue Class Component](https://github.com/vuejs/vue-class-component/issues/109)


## Options for admin/personal admin sites
* https://w3layouts.com/preview/?l=/modern-admin-panel-flat-bootstrap-responsive-web-template/
*


## Components
* Calendar - [Date Picker](https://github.com/charliekassel/vuejs-datepicker) -
