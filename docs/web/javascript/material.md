# Notes for material.angular.io

* Using with autocomplete
    * displayWith issue: don't have access to the host component.
        * [Issue 3308](https://github.com/angular/material2/issues/3308)
        * [Issue 3359](https://github.com/angular/material2/issues/3359)
    * Fix/workaround below.
```ts
  get displayName() {
    return (val) => val ? this.accounts.filter( (account) => account.account_uuid === val)[0].full_name : undefined;
  }
```
