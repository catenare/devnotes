# Notes about learning reactjs

## Setup React from Scratch with TypeScript Support using Parcel

- https://github.com/parcel-bundler/awesome-parcel

* https://github.com/linbudu599/Parcel-Tsx-Template

- [PostCss](https://postcss.org/)
- [TypeScript](https://www.typescriptlang.org/index.html)

* Create directory
* Create Directory Structure

  - public
    - index.html
  - src
    - App.scss
    - App.tsx
    - index.tsx

  * .babelrc
  * .gitignore

* Create _postcss.config.js_ file

```json
module.exports = {
  plugins: [
    require("autoprefixer"),
    require("postcss-nested"),
    require("postcss-scss"),
    require("postcss-jsx"),
  ],
};
```

- Setup _package.json_ - `yarn install -y`

* Install required packages:

```json
{
  "name": "taskbox",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "devDependencies": {
    "@babel/cli": "^7.8.4",
    "@typescript-eslint/eslint-plugin": "^2.30.0",
    "@typescript-eslint/parser": "^2.30.0",
    "babel-eslint": "^10.1.0",
    "eslint-config-prettier": "^6.11.0",
    "eslint-config-react-app": "^5.2.1",
    "eslint-plugin-flowtype": "^4.7.0",
    "eslint-plugin-html": "^6.0.2",
    "eslint-plugin-import": "^2.20.2",
    "eslint-plugin-jsx-a11y": "^6.2.3",
    "eslint-plugin-react": "^7.19.0",
    "eslint-plugin-react-hooks": "^4.0.0",
    "node-sass": "^4.14.0",
    "parcel-bundler": "^1.12.4"
  },
  "dependencies": {
    "@babel/core": "^7.9.6",
    "@babel/preset-env": "^7.9.6",
    "@babel/preset-react": "^7.9.4",
    "@babel/preset-typescript": "^7.9.0",
    "@jest/core": "^25.5.4",
    "@types/node": "^13.13.4",
    "@types/react": "^16.9.34",
    "@types/react-dom": "^16.9.7",
    "@types/react-router-dom": "^5.1.5",
    "babel-jest": "^25.5.1",
    "eslint": "^6.8.0",
    "jest": "^25.5.4",
    "prettier": "^2.0.5",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "typescript": "^3.8.3"
  }
}
```

- Create _tsconfig.json_ file - `npx tsc --init`

* Can now start with a basic react tutorial

## Routing is very different from what's available in books and tutorials

- [Documentation for Routing](https://reacttraining.com/react-router/)
- [CSS Tricks: React Router 4](https://css-tricks.com/react-router-4/)
  - Good code examples

## Notes from rangle.io web chat

- Tools: react, redux, express (optional)
- Tools
  - webpack w/ babel
  - PostCSS/CSSNext
  - Testing - karma, mocha, chai
  - Linting tools - js and css/sass (eslint/stylelint)
  - Enzyme - component testing (?)
  - Robot e2e test framework - python framework. natural language. connect to ci
- HelmetJS - security from cross-scripting
- Dev tools
  - npm start - run in production mode
  - npm dev - dev mode - dev tools connected.
- Components
  - atomic design

## General Notes

- [React Typescript Samples](https://github.com/Lemoncode/react-typescript-samples)
- Render raw html in reactjs - `<p className="article-row-content-description" dangerouslySetInnerHTML={{__html: props.post.excerpt.rendered}} />`

## Development

- [Cross Origin Errors](https://reactjs.org/docs/cross-origin-errors.html)

```
Source maps
Some JavaScript bundlers may wrap the application code with eval statements in development. (For example Webpack will do this if devtool is set to any value containing the word “eval”.) This may cause errors to be treated as cross-origin.
If you use Webpack, we recommend using the cheap-module-source-map setting in development to avoid this problem.
```

- Import react - ['Cannot read property of createElement of undefined'](https://stackoverflow.com/questions/37360202/uncaught-in-promise-typeerror-cannot-read-property-createelement-of-undefin)

```
import { React, Component } from 'react';
needs to be
import React, { Component } from 'react';
```

### exporting stateless component

```jsx
import React from "react";
import ReactDOM from "react-dom";

const data = [
  {
    name: "Baked Salmon",
    ingredients: [
      { name: "Salmon", amount: 1, measurement: "l lb" },
      { name: "Pine Nuts", amount: 1, measurement: "cup" },
      { name: "Butter Lettuce", amount: 2, measurement: "cups" },
      { name: "Yellow Squash", amount: 1, measurement: "med" },
      { name: "Olive Oil", amount: 0.5, measurement: "cup" },
      { name: "Garlic", amount: 3, measurement: "cloves" },
    ],
    steps: [
      "Preheat the oven to 350 degrees.",
      "Spread the olive oil around a glass baking dish.",
      "Add the salmon, garlic, and pine nuts to the dish.",
      "Bake for 15 minutes.",
      "Add the yellow squash and put back in the oven for 30 mins.",
      "Remove from oven and let cool for 15 minutes. Add the lettuce and serve.",
    ],
  },
  {
    name: "Fish Tacos",
    ingredients: [
      { name: "Whitefish", amount: 1, measurement: "l lb" },
      { name: "Cheese", amount: 1, measurement: "cup" },
      { name: "Iceberg Lettuce", amount: 2, measurement: "cups" },
      { name: "Tomatoes", amount: 2, measurement: "large" },
      { name: "Tortillas", amount: 3, measurement: "med" },
    ],
    steps: [
      "Cook the fish on the grill until hot.",
      "Place the fish on the 3 tortillas.",
      "Top them with lettuce, tomatoes, and cheese",
    ],
  },
];

const Menu = ({ title, recipes }) => (
  <article>
    <header>
      <h1>{title}</h1>
    </header>
    <div className="recipes">
      {recipes.map((recipe, i) => (
        <Recipe
          key={i}
          name={recipe.name}
          ingredients={recipe.ingredients}
          steps={recipe.steps}
        />
      ))}
    </div>
  </article>
);

const Recipe = ({ name, ingredients, steps }) => (
  <section id={name.toLowerCase().replace(/ /g, "-")}>
    <h1>{name}</h1>
    <ul className="ingredients">
      {ingredients.map((ingredient, i) => (
        <li key={i}>{ingredient.name}</li>
      ))}
    </ul>
    <section className="instructions">
      <h2>Cooking Instructions</h2>
      {steps.map((step, i) => (
        <p key={i}>{step}</p>
      ))}
    </section>
  </section>
);

const list = () => <Menu recipes={data} title="Delicious Recipes" />;

export { list };
```

- In Routing

```tsx
import * as React from "react";
import {
  BrowserRouter,
  HashRouter,
  Redirect,
  Route,
  Switch,
} from "react-router-dom"; // eslint-disable-line
import { Hello } from "./components/Home/Hello";
import { list } from "./components/Ingredients/ingredients";

const AppRoute = () => (
  // eslint-disable-line
  <HashRouter>
    <main>
      <Switch>
        <Route path="/" exact component={list} />
        <Redirect to="/" />
      </Switch>
    </main>
  </HashRouter>
);

export { AppRoute };
```

## Using typescript

- tsConfig that works with `(color) => (color.id !== id) ? color : {...color, rating},`. Was causing issues when transpiling

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "lib": ["es6", "dom"],
    "jsx": "react",
    "allowJs": true,
    "pretty": true,
    "diagnostics": true,
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true,
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  },
  "exclude": ["node_modules"]
}
```

# Redux

## Resources

- [Documentation](https://redux.js.org)
- [Getting Started With Redux](https://egghead.io/courses/getting-started-with-redux)
  - [Class Notes](https://github.com/tayiorbeii/egghead.io_redux_course_notes)
- [Build React Applications with Idiomatic Redux](https://egghead.io/courses/building-react-applications-with-idiomatic-redux)
  - [Class Notes](https://github.com/tayiorbeii/egghead.io_idiomatic_redux_course_notes)

## Code Examples.

- Redux Implementation - implement redux from scratch (how it all works together). Only requires React.

```js
const createStore = (reducer) => {
  let state: number;
  let listeners = [];

  const getState = () => state;

  const dispatch = (action) => {
    state = reducer(state, action);
    listeners.forEach((listener) => listener());
  };

  const subscribe = (listener) => {
    listeners.push(listener);
    return () => {
      listeners = listeners.filter((l) => l !== listener);
    };
  };

  dispatch({});

  return { getState, dispatch, subscribe };
};

const counter = (state: number = 0, action) => {
  switch (action.type) {
    case "INCREMENT":
      state = state + 1;
      return state;
    case "DECREMENT":
      return state - 1;
    default:
      return state;
  }
};

const store = createStore(counter);
const unsub = store.subscribe(() => console.log(store.getState()));

const el = document.getElementById("blog");

const Counter = (props) => {
  const { value, onIncrement, onDecrement } = props;
  return (
    <div>
      <h1>Value: {value}</h1>
      <button className="button large" onClick={onIncrement}>
        +
      </button> &nbsp;
      <button className="button large" onClick={onDecrement}>
        -
      </button>
    </div>
  );
};

const render = () =>
  ReactDOM.render(
    <Counter
      value={store.getState()}
      onIncrement={() => store.dispatch({ type: "INCREMENT" })}
      onDecrement={() => store.dispatch({ type: "DECREMENT" })}
    />,
    // <AppRoute />,
    el
  );

render();

const renderUnsub = store.subscribe(render);
```
