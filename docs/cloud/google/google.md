# Using Google Cloud Services and Functions (Firebase)

## Issues
* Using TypeScript
    * Node version online is v6.11.5
    * Be sure to install firebase-tools in this version
    * Samples is incorrect
        * tsconfig.json is incorrect
            * add "dom" to "lib". Should be: "lib": ["es6", "dom"]
            * [Github Issues](https://github.com/firebase/functions-samples/issues/310) 
