# Developer Journal.
## Vuejs with vue-cli
* Good Example Project - https://github.com/catenare/lookfindmeadmin2
* Proxy config - *vue.config.js*
	* Can add webpack configuration using *ConfigureWebpack* 
## LookFindMeAdmin site
* Using Vuejs with vue-cli 3
* Monday 11 June 2018 @ 15:23
	* Got rxjs ajax to work with VueJs.
		* `import {ajax} from "rxjs/ajax";`
	* Admin command line client
		* `pipenv install -e .` - installs the command line client locally.
		* `lookfindme` - list of commands available.
		* `lookfindme inser_site` - read info from json document (app_data.json, industries.json) and populate database table(s).
		* Settings table has multiple json objects to store setting data. Don't expect to do any reporting on those fields. Mostly text and will be accessed only at build/create time.
		* Settings table saves all changes. Access to the latest settings if via the site_uuid and latest version based on updated_at column.
	* All components are under the settings.vue component
		* Need to figure out how to get the updated information back from the components.
		* Show everything as fields.
		* Update the database after the fields have been updated.
	* Add form array in VueJS - (v-model-array-multiple-input)[https://stackoverflow.com/questions/34825065/vuejs-v-model-array-in-multiple-input]
```ts
new Vue({
  el: '#app',
  data: {
    finds: []
  },
  methods: {
    addFind: function () {
      this.finds.push({ value: '' });
    }
  }
});
```
```html
<div id="app">
  <h1>Finds</h1>
  <div v-for="find in finds">
    <input v-model="find.value">
  </div>
  <button @click="addFind">
    New Find
  </button>
</div>
```
## Python Notes:
list comprehension: list = []
## https://surmon-china.github.io/vue-quill-editor/ - vue-quill-editor - able to set options via :options directive.