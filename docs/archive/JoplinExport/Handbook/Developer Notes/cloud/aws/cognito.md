---
title: cognito
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# AWS Cognito

## Notes
* Trying to use aws-amplify with Typescript
* Issues with typescript definitions
* Adding @types/node for aws-sdk. See if that will help [aws-sdk-js#Usage with TypeScript](https://github.com/aws/aws-sdk-js)
  * [tsconfig](https://github.com/aws/aws-sdk-js/blob/master/ts/tsconfig.json)
* Result
  * `npm install --save-dev @types/node`
  * `npm install aws-amplify`

## Resources
* [Auth Guide](https://aws.github.io/aws-amplify/media/authentication_guide.html)
* [Custom UI for Cognito with aws-amplify](https://shellmonger.com/2018/01/17/building-a-custom-ui-for-amazon-cognito-with-aws-amplify/)
* [AWS Documentation](https://aws.github.io/aws-amplify/)
* `tsconfig.json`
```
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "jsx": "preserve",
    "noImplicitAny": false,
    "noImplicitThis": true,
    "allowJs": true,
    "pretty": true,
    "diagnostics": true,
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true,
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  },
  "exclude": [
    "node_modules"
  ],
  "awesomeTypescriptLoaderOptions": {
    "useWebpackText": true,
    "useTranspileModule": true,
    "useBable": true,
    "useCache": true,
    "doTypeCheck": true,
    "forkChecker": true
  }
}
```

### Steps
### Configure the client
* 
