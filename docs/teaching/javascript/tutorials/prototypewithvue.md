# Building a protype with Vue and Marvel
* *Based on [How to Create an App Prototype Using CSS and JavaScript](https://webdesign.tutsplus.com/tutorials/how-to-create-an-app-prototype-using-css-and-javascript--cms-29062)*
* Want to build a demo prototype but rather than using vanilla es6, Use Vue.

## Getting Started
* Create single file component
    1. Create component folder. - *vue/components/MarvelProto*
    1. Create 4 files in folder. *index.vue*, *script.ts*, *template.html* and *styles.scss*
        * We are using TypeScript and SASS
    1. Include all the parts of the single file component in *index.vue*
```html
    <template src="./template.html"></template>
    <script lang="ts" src="./script.ts"></script>
    <style scoped lang="scss" src="./style.scss"></style>
``` 
* Download Marvel's *devices.css* from github. [Devices.css](https://github.com/marvelapp/devices.css)
    * Download the zip file.
    * Expand the zip file and copy the *assets/scss* folder to your *MarvelProto* component.
    * Import *devices.scss* into the *style.scss* file.
* Wire the component into your current application.
    * In main *app.js* file
        * Import MarvelProto - *import MarvelProto from '../vue/components/MarvelProto'*
        * Add to global component list - *Vue.component('marvelproto', MarvelProto)* - can't get local import to work.
        * Add component to current root element in *vue/components/ContactForm/template.html*.
```html
<div class="contact-form">
    <marvelproto></marvelproto>
    <pre>
        {{ $data }}
    </pre>
</div>
```
## Getting the user data
* [Axios with Vue](https://alligator.io/vuejs/rest-api-axios/)
* We will be retrieving random users from [RandomUser API](https://randomuser.me/api/) - https://randomuser.me/api/
    * Service for testing your code calling APIs
* Going to use *axios* with *vue* - *script.ts* file.
* Get the data when the component is created.
```js
import axios from 'axios'

export default {

    data: () => (
        {
            errors: [],
            greeting: "Hello World",
            users: [],
        }
    ),

  created() {
        axios(
            {
                method: "GET",
                url: "https://randomuser.me/api/?results=30",
            })
            .then(  (response) => {
                this.users = response.data;
            })
            .catch((e) => {
                this.errors.push(e);
            });
    },
}
```


