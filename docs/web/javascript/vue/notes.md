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
