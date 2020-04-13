# Building a protype with Vue and Marvel
* *Based on [How to Create an App Prototype Using CSS and JavaScript](https://webdesign.tutsplus.com/tutorials/how-to-create-an-app-prototype-using-css-and-javascript--cms-29062)*
* We are building this exact prototype using Vue and building it as a single file component.
* Have to use the *marvel-device nexus5* for it work properly.

```html
<div class="contact-form">
    <marvelproto></marvelproto>
</div>
```
## JavaScript
```js
import axios from 'axios'

const transOriginNames = {
    MozTransformOrigin    : "MozTransformOrigin",
    msTransformOrigin     : "msTransformOrigin",
    transformOrigin       : "transformOrigin",
    webkitTransformOrigin : "webkitTransformOrigin",
};

let screen_scroll = this;
let modal = this;

export default {

    data: () => (
        {
            avatar: {
                img: "",
                name: "",
            },
            errors: [],
            greeting: "User List",
            isActive: false,
            isLoaded: false,
            users: [],
        }
    ),

  mounted() {
        axios(
            {
                method: "GET",
                url: "https://randomuser.me/api/?results=30",
            })
            .then(  (response) => {
                this.users = response.data.results;
                this.isLoaded = true;
            })
            .catch((e) => {
                this.errors.push(e);
            });
        screen_scroll = this.$el.querySelector(".screen-scroll");
        modal = this.$el.querySelector(".modal");
    },

    methods: {
        fullname: (user) => {
            return user.name.first + " " + user.name.last;
        },
        hideModal() {
            this.isActive = false;
        },
        showModal(e) {
            const target = e.target;
            this.avatar.img = target.getAttribute("data-pic");
            this.avatar.name = target.getAttribute("data-name");
            this.avatar.email = target.getAttribute("data-email");
            const targetCoords = target.getBoundingClientRect();

            if (target.nodeName === "IMG") {
                for (let name in transOriginNames) {
                    modal.style[name] = (target.offsetLeft + (targetCoords.width / 2)) + "px "
                        + ((target.offsetTop + (targetCoords.height / 2)) - screen_scroll.scrollTop) + "px";
                }
            }
            this.isActive = true;
        },
    },
};

```

## Template
```html
<div class="marvel-device nexus5">
    <div class="top-bar"></div>
    <div class="sleep"></div>
    <div class="volume"></div>
    <div class="camera"></div>
    <div class="screen"  v-bind:class="{active: isActive}">
        <div class="screen-scroll">
            <h3 class="title">{{greeting}}</h3>
            <div class="loader" v-bind:class="{hide: isLoaded}">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" aria-hidden="true">
                    <circle cx="50" cy="37" r="7"/>
                    <circle cx="62.5" cy="43.5" r="7"/>
                    <circle cx="62.5" cy="56.5" r="7"/>
                    <circle cx="50" cy="65" r="7"/>
                    <circle cx="37.5" cy="56.5" r="7"/>
                    <circle cx="37.5" cy="43.5" r="7"/>
                </svg>
            </div>
            <ul class="users" v-bind:class="{show: isLoaded}">
                <li v-for="user in users" @click.stop.prevent="showModal">
                    <img :src="user.picture.medium"
                         :data-pic="user.picture.large"
                         :data-name="fullname(user)"
                         :data-email="user.email"
                    >
                    <span class="user-name">{{user.name.first}}</span>
                </li>
            </ul>
        </div>
        <div class="modal" @click.stop.prevent="hideModal">
            <div class="avatar">
                <img :src="avatar.img" :alt="avatar.name">
            </div>
            <div class="profile">
                <h3 class="profile_name">{{avatar.name}}</h3>
                <a href="#" class="profile__email">{{avatar.email}}</a>
                <button>Follow</button>
                <p class="profile__info">Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus. Etiam porta sem malesuada magna mollis euismod.</p>
           </div>
        </div>
    </div>
</div>
```
## Stylesheet in SCSS
```scss
@import 'marvel/devices';

// ==========================================================
// DEMO STYLES
// ==========================================================

$bg: #91999f;

html,
body { height: 100%; }

body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  background: $bg;
}

// ==========================================================
// REQUIRED STYLES
// ==========================================================

:root {
  --primary-color: #2c3942;
  --secondary-color: #1192ff;
  --tertiary-color: #997ac0;
  --button-bg: var(--tertiary-color);
  --material-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  --screen-height: 568px;
  --screen-width: 320px;
}

* {
  &:before,
  &:after {
    box-sizing: inherit;
  }
}

html,
input {
  box-sizing: border-box;
}

button {
  appearance: none;
  border: 2px solid var(--button-bg);
  border-radius: 100px;
  margin: 10px 0;
  padding: 10px 0;
  transition: 200ms background cubic-bezier(.4, 0, .2, 1);
  font-weight: 400;
  background: transparent;
  color: white;
  &:hover,
  &:focus {
    cursor: pointer;
    background: var(--button-bg);
  }
  &:focus {
    outline: none;
  }
}

.screen {
  position: relative;
  background: var(--primary-color);
}

.screen-scroll {
  height: 100%;
  overflow: scroll;
}

.title {
  font-family: 'Roboto', sans-serif;
  font-size: 1em;
  font-weight: 300;
  text-transform: uppercase;
  color: white;
}

.users {
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  margin: 0;
  padding: 0;

  li {
    padding: 5px;
    width: 30%;
    opacity: 0;
  }

  img {
    border-radius: 80%;
    box-shadow: var(--material-shadow);

    &:hover {
      cursor: pointer;
    }
  }
}

.modal {
  border-radius: 100%;
  height: var(--screen-height);
  pointer-events: none;
  position: absolute;
  top: 0;
  left: 0;
  overflow: scroll;
  transform: scale(0) translateZ(0);
  transition-duration: 640ms;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-property: transform, opacity, border-radius;
  width: var(--screen-width);
  background-color: var(--primary-color);
  opacity: 0;
}

.avatar {
  position: relative;

  &::after {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(180deg, rgba(255, 255, 255, 0) 0%, var(--primary-color) 98%);
  }

  img {
    display: inline-block;
    width: 100%;
    max-width: 100%;
  }
}

.user-name {
  display: block;
  font-family: 'Roboto', sans-serif;
  font-weight: 300;
  text-align: center;
  font-size: 0.875em;
  text-transform: capitalize;
}

.profile {
  display: flex;
  flex-direction: column;
  padding: 0 1rem;
  transition: 200ms transform 100ms cubic-bezier(0.4, 0, 0.2, 1);
  transform: translateY(-100%);
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
}

.profile__name {
  margin: 0;
  font-family: 'Roboto', sans-serif;
  font-weight: 300;
  text-transform: capitalize;
}

.profile__email {
  display: inline-block;
  margin: 5px 0;
  font-family: 'Roboto', sans-serif;
  font-weight: 300;
  text-decoration: none;
  color: inherit;
}

.profile__info {
  font-family: 'Roboto', sans-serif;
  font-weight: 300;
}

// ==========================================================
// LOADER
// ==========================================================

$loader-count: 6;
$loader-proportion: 200px;
$loader-color: #00AABB;
$stagger: 0.1875s;
$animation_config: (
        name: expand-out,
        duration: 600ms,
        timing: cubic-bezier(0.66, 0.14, 0.83, 0.67),
        iteration: infinite,
        direction: alternate,
        fill-mode: both
);

@function sh-setup($config) {
  @return zip(map-values($config)...);
}

.loader {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  bottom: 0;
  transform: translateY(-50%);
}

.loader svg {
  position: relative;
  width: $loader-proportion;
  height: $loader-proportion;
  circle {
    animation: sh-setup($animation_config);
    position: absolute;
    transform: scale(0);
    transform-origin: center center;
    fill: $loader-color;
  }
}

@for $i from 1 through $loader-count {
  .loader circle:nth-of-type(#{$i}) {
    animation-delay: $i * $stagger;
    fill: lighten($loader-color, $i * 3%);
  }
}

// ==========================================================
// STATES
// ==========================================================

$user-count: 30;
$duration: 200ms;
$stagger_delay: 0.0125s;
$easing: cubic-bezier(0.66, 0.14, 0.83, 0.67);

.loader.hide {
  display: none;
}

.users.show {
  > * {
    animation-duration: $duration;
    animation-name: fade-in;
    animation-fill-mode: both;
    animation-timing-function: $easing;
    opacity: 1;

    > * {
      animation-duration: $duration;
      animation-name: expand-out;
      animation-fill-mode: both;
      animation-timing-function: $easing;
    }

    @for $i from 1 through $user-count {
      &:nth-of-type(#{$i}) {
        animation-delay: ($stagger_delay * $i);
        > * {
          animation-delay: ($stagger_delay * $i);
        }
      }
    }
  }
}

.screen.active {
  .screen-scroll {
    overflow: hidden;
  }

  .modal {
    border-radius: 0;
    pointer-events: auto;
    transform: scale(1) translateZ(0);
    opacity: 1;
  }

  .profile {
    transform: translateY(0);
  }
}

// ==========================================================
// KEYFRAMES
// ==========================================================

@keyframes fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes expand-out {
  from { transform: scale(0); }
  to   { transform: scale(1); }
}

```

## Getting Started
### Creating the project
* Create a new vue project with the vue-cli
    * `vue init webpack-simple marvel-prototype`
* Add the additional npm packages.
    * awesome-typescript-loader  > We're using typescript
    * axios > ajax calls
    * babel-env
    * babel-preset-env
    * babel-plugin-transform-class-properties
    * babel-plugin-transform-decorators
    * postcss-loader
    * postcss-cssnext  > issue with css variables
    * vue-hot-reload-api
    * tslint
    * typescript - create config file
    * eslint
    * eslint-config-standard
    * style-loader

* Configure work environment
    * typescript
        * tslint - `./node_modules/.bin/tslint --init` - Generates a *tslint.json* file.
        * tsc - `./node_modules/.bin/tsc --init` - Generates *tsconfig.json* file.
```json
"compilerOptions": {
    "target": "es5",
    "module": "es2015",
    //    "strict": true  
    "allowSyntheticDefaultImports": true,
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
}
```
* eslint
* babel
    * Create .babelrc file.
```json
{
  "presets": [
    ["env",{
      "targets": {
        "browsers": ["last 2 versions", "safari >= 7"]
      }
    }
    ]
  ],
  "plugins": [
    "transform-class-properties",
    "transform-decorators"
  ]
}
```
* Create *postcss.config.js*
* You need to set this up to have the future css vars work.
```js
module.exports = {
  plugins: {
    'postcss-cssnext': {}
  }
}
```
* Configure eslint
```json
{
    "extends": "standard"
}
```

### Update your webpack config
* Add *scss* processing section.
```js
      {
        test: /\.scss/,
        loaders: [
          'style-loader',
          'css-loader',
          'sass-loader'
        ]
      }
```
* Add typescript processing in vue-loader section.
```js
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
                loader: 'sass-loader'
              }
            ],
            ts: 'awesome-typescript-loader'
          }
        }
      },
```
* Add typescript processing section.
```js
      {
        test: /\.ts$/,
        loader: 'awesome-typescript-loader',
        exclude: /node_modules/

      },
```

### Create Vue Component folder
* *./src/components* 
* Create *MarvelProto* in *components*.
* Create files for the component
    * MarvelProto.vue
    * template.html
    * script.ts
    * style.scss
* Edit *MarvelProto.vue*

### Download and add Marvel CSS for devices.
* Download *https://github.com/marvelapp/devices.css/archive/master.zip*
* Unzip and copy *devices.scss* and *mixins.scss* from *devics.css-master/assets/scss/* into *src/assets/scss* folder.
* Add the HTML to the MarvelProto *template.html* file.

### Add MarvelProto component as main component.
* Import MarvelProto - `import MarvelProto from './components/MarvelProto/MarvelProto.vue'`
* Place it as the main component.
```js
new Vue({
  el: '#app',
  render: h => h(MarvelProto)
})
```
### Setup Demo Content
* in *MarvelProto/script.ts*, create a *msg* variable.
```js
export default {

    data: () => (
        {
            msg: "Hello World"
        }
    )
}
```
* Show the message in the template.
```html
<div class="marvel-device iphone6 silver">
    <div class="top-bar"></div>
    <div class="sleep"></div>
    <div class="volume"></div>
    <div class="camera"></div>
    <div class="sensor"></div>
    <div class="speaker"></div>
    <div class="screen">
        {{ msg }}
    </div>
    <div class="home"></div>
    <div class="bottom-bar"></div>
</div>
```
* Include the device.scss in your style sheet.
* `@import 'scss/devices';`

* Start your development server.
* `npm run dev`
[image of plain phone]

## Component Code
### Retrieve the list of users using [axios](https://github.com/mzabriskie/axios).
* in MarvelProto/script.ts
* import axios
* Create code to pull users from random api.
```js
import axios from 'axios';

export default {

    data: () => (
        {
            errors: [],
            msg: "Hello World",
            users: [],

        }
    ),

    mounted() {
        axios(
            {
                method: "GET",
                url: "https://randomuser.me/api/?results=30",
            })
            .then(  (response) => {
                this.users = response.data.results;
                this.isLoaded = true;
            })
            .catch((e) => {
                this.errors.push(e);
            });
    },
};
```
* Update *template.html* to show users
    * Add for loop for users in `<ul class="users">`
```html
<div class="marvel-device iphone6plus black">
    <div class="top-bar"></div>
    <div class="sleep"></div>
    <div class="volume"></div>
    <div class="camera"></div>
    <div class="screen">
        <div class="screen-scroll">
            <h3 class="title">{{ msg }}</h3>
            <div class="loader">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" aria-hidden="true">
                    <circle cx="50" cy="37" r="7"/>
                    <circle cx="62.5" cy="43.5" r="7"/>
                    <circle cx="62.5" cy="56.5" r="7"/>
                    <circle cx="50" cy="65" r="7"/>
                    <circle cx="37.5" cy="56.5" r="7"/>
                    <circle cx="37.5" cy="43.5" r="7"/>
                </svg>
            </div>
            <ul class="users">
                <li v-for="user in users">
                    <img :src="user.picture.medium"
                         :data-pic="user.picture.large"
                         :data-name="fullname(user)"
                         :data-email="user.email"
                    >
                    <span class="user-name">{{user.name.first}}</span>
                </li>
            </ul>

        </div>
        <div class="modal">
            <div class="avatar"></div>
            <div class="profile"></div>
        </div>
    </div>
</div>
```
* Hide Loader and show users.
    * Hide loader: `<div class="loader" v-bind:class="{hide: isLoaded}">`
    * Show Users: `<ul class="users" v-bind:class="{show: isLoaded}">`

* Create Modal
```html
        <div class="modal" @click.stop.prevent="hideModal">
            <div class="avatar">
                <img :src="avatar.img" :alt="avatar.name">
            </div>
            <div class="profile">
                <h3 class="profile_name">{{avatar.name}}</h3>
                <a href="#" class="profile__email">{{avatar.email}}</a>
                <button>Follow</button>
                <p class="profile__info">Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus. Etiam porta sem malesuada magna mollis euismod.</p>
            </div>
        </div>
```
* Add code to show and hide the Modal under Methods.
```js
        hideModal() {
            this.isActive = false;
        },
        showModal(e) {
            const target = e.target;
            this.avatar.img = target.getAttribute("data-pic");
            this.avatar.name = target.getAttribute("data-name");
            this.avatar.email = target.getAttribute("data-email");
            const targetCoords = target.getBoundingClientRect();

            if (target.nodeName === "IMG") {
                for (let name in transOriginNames) {
                    modal.style[name] = (target.offsetLeft + (targetCoords.width / 2)) + "px "
                        + ((target.offsetTop + (targetCoords.height / 2)) - screen_scroll.scrollTop) + "px";
                }
            }
            this.isActive = true;
        },
```
