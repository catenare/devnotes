# Notes about learning reactjs

## Routing is very different from what's available in books and tutorials
* [Documentation for Routing](https://reacttraining.com/react-router/)
* [CSS Tricks: React Router 4](https://css-tricks.com/react-router-4/)
    * Good code examples

## Notes from rangle.io web chat
* Tools: react, redux, express (optional)
* Tools
    * webpack w/ babel
    * PostCSS/CSSNext
    * Testing - karma, mocha, chai
    * Linting tools - js and css/sass (eslint/stylelint)
    * Enzyme - component testing (?)
    * Robot e2e test framework - python framework. natural language. connect to ci
* HelmetJS - security from cross-scripting
* Dev tools
    * npm start - run in production mode
    * npm dev - dev mode - dev tools connected.
* Components
    * atomic design

## General Notes
* [React Typescript Samples](https://github.com/Lemoncode/react-typescript-samples)

## Development
* [Cross Origin Errors](https://reactjs.org/docs/cross-origin-errors.html)
```
Source maps
Some JavaScript bundlers may wrap the application code with eval statements in development. (For example Webpack will do this if devtool is set to any value containing the word “eval”.) This may cause errors to be treated as cross-origin.
If you use Webpack, we recommend using the cheap-module-source-map setting in development to avoid this problem.
```

* Import react - ['Cannot read property of createElement of undefined'](https://stackoverflow.com/questions/37360202/uncaught-in-promise-typeerror-cannot-read-property-createelement-of-undefin)
```
import { React, Component } from 'react';
needs to be
import React, { Component } from 'react';
```

### exporting stateless component
```jsx
import React from "react";
import ReactDOM  from "react-dom";

const data = [
  {
      "name": "Baked Salmon",
      "ingredients": [
          { "name": "Salmon", "amount": 1, "measurement": "l lb" },
          { "name": "Pine Nuts", "amount": 1, "measurement": "cup" },
          { "name": "Butter Lettuce", "amount": 2, "measurement": "cups" },
          { "name": "Yellow Squash", "amount": 1, "measurement": "med" },
          { "name": "Olive Oil", "amount": 0.5, "measurement": "cup" },
          { "name": "Garlic", "amount": 3, "measurement": "cloves" }
      ],
      "steps": [
          "Preheat the oven to 350 degrees.",
          "Spread the olive oil around a glass baking dish.",
          "Add the salmon, garlic, and pine nuts to the dish.",
          "Bake for 15 minutes.",
          "Add the yellow squash and put back in the oven for 30 mins.",
          "Remove from oven and let cool for 15 minutes. Add the lettuce and serve."
      ]
  },
  {
      "name": "Fish Tacos",
      "ingredients": [
          { "name": "Whitefish", "amount": 1, "measurement": "l lb" },
          { "name": "Cheese", "amount": 1, "measurement": "cup" },
          { "name": "Iceberg Lettuce", "amount": 2, "measurement": "cups" },
          { "name": "Tomatoes", "amount": 2, "measurement": "large"},
          { "name": "Tortillas", "amount": 3, "measurement": "med" }
      ],
      "steps": [
          "Cook the fish on the grill until hot.",
          "Place the fish on the 3 tortillas.",
          "Top them with lettuce, tomatoes, and cheese"
      ]
  }
]

const Menu = ({title, recipes}) => (
  <article>
    <header>
      <h1>{title}</h1>
    </header>
    <div className="recipes">
      {recipes.map((recipe, i) => <Recipe key={i} name={recipe.name} ingredients={recipe.ingredients} steps={recipe.steps} />)}
    </div>
  </article>
)

const Recipe = ({name, ingredients, steps }) =>
<section id={name.toLowerCase().replace(/ /g, "-")}>
  <h1>{name}</h1>
  <ul className="ingredients">
    {ingredients.map((ingredient, i) => <li key={i}>{ingredient.name}</li>)}
  </ul>
  <section className="instructions">
    <h2>Cooking Instructions</h2>
    {steps.map((step, i) => <p key={i}>{step}</p>)}
  </section>
</section>

const list = () => <Menu recipes={data} title="Delicious Recipes" />

export {list};
```
* In Routing

```tsx
import * as React from "react";
import {BrowserRouter, HashRouter, Redirect, Route, Switch } from "react-router-dom"; // eslint-disable-line
import {Hello} from "./components/Home/Hello";
import {list} from "./components/Ingredients/ingredients";

const AppRoute = () => ( // eslint-disable-line
  <HashRouter>
    <main>
      <Switch>
        <Route path="/" exact component={list} />
        <Redirect to="/" />
      </Switch>
    </main>
  </HashRouter>
);

export {AppRoute};
```
