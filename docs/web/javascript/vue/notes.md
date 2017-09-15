# General notes while developing with Vue

## Missing filters
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
