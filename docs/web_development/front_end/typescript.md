# Typescript Notes
## tslint
* [tslint](https://github.com/palantir/tslint/blob/master/docs/usage/rule-flags/index.md) - how to disable rules per line or section. // tslint:disable-line 

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

