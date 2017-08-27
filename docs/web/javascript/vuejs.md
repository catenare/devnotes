# Vuejs Notes
## Webpack Configuration
* Read the (vue-loader)[https://vue-loader.vuejs.org/en/] docs.
    * Especially the section on loaders.
* Vue npm modules to include:
    * vue
    * vue-hot-reload-api
    * vue-templates-compiler
    * vue-html-loader
    * vue-style-loader
    * eslint-plugin-vue
* TypeScript
    * Edit your `tsconfig.json` file. I removed all the comments because it caused problems.
    * In your components, be sure to include *lang="ts"* in your script tag.
    * I'm using *awesome-typescript-loader*. Add it as a loader option in your vue section of webpack.
* eslint
    * [Vue eslint plugin](https://github.com/vuejs/eslint-plugin-vue)
    * add *"plugin:vue/recommended"* to extends section

## Including Foundation with webpack and vue
* `npm install foundation-sites jquery motion-ui what-input`
    * [vue-foundation](https://github.com/vue-foundation)
* Getting the scss to work requires some configuration

## Notes
* Make sure to include *.vue* as part of filename. Can cause problems when importing.   

## Snippets
* Webpack snippet
```javascript
          {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: {
          loaders: {
            ts: 'awesome-typescript-loader'
          },
          extractCSS: true
        }
      },
```
* tsconfig.json file
```json
{
  "compilerOptions": {
    "target": "es2016",
    "module": "ESNext",
    "lib": [
      "dom",
      "es2016",
      "es2015.promise"
    ],
    "strict": true,
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true,
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```
