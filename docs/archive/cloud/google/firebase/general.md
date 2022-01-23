# Google Firebase
* Using Google Firebase for hosting

## Setup notes
* Setting up hosting
	* Folder is "dist".
	* *firebase.json* should contain the following configuration. Documentation does not contain these notes. Results in an error. [Firebase Issue 367](https://github.com/firebase/firebase-tools/issues/367)
```json
{
  "hosting": {
    "public": "dist",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  }
}
```
## Process
1. Install firebase tools - `npm install -g firebase-tools`
2. Login to firebase - `firebase login`
3. Create project in firebase console.
4. In project directory (Project/dist) - `firebase init`
5. Select firebase project
6. Select hosting
7. Be sure to configure *firebase.json* correctly
8. Test with `firebase serve`
9. Deploy with `firebase deploy`
10. Configure domain information.

## Issues
* Using TypeScript
    * Node version online is v6.11.5
    * Be sure to install firebase-tools in this version
    * Samples is incorrect
        * tsconfig.json is incorrect
            * add "dom" to "lib". Should be: "lib": ["es6", "dom"]
            * [Github Issues](https://github.com/firebase/functions-samples/issues/310)
