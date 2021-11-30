---
title: typescript
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Typescript Notes
## Resources
* [Typescript Language](https://www.typescriptlang.org)
* [TypeScript Notation](https://2ality.com/2018/04/type-notation-typescript.html)
* [TypeScript React Cheetsheet](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet)
* [React Typescript Guide](https://github.com/piotrwitek/react-redux-typescript-guide)
## tslint
* ~~[Tslint](https://github.com/palantir/tslint/blob/master/docs/usage/rule-flags/index.md) - how to disable rules per line or section. // tslint:disable-line~~ Use eslint

* Import json file into a typescript product
* [How to Import json into TypeScript](https://hackernoon.com/import-json-into-typescript-8d465beded79)
* Declare json in your typings file
  * Vue - vue-shim.d.ts or index.d.ts
```js
declare module "*.json" {
    const value: any;
    export default value;
}
``

## Issues
* Dealing with `this`
* [This in typescript](https://github.com/Microsoft/TypeScript/wiki/'this'-in-TypeScript)
