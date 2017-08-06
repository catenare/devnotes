# Figuring out RXJS

## Notes
* Getting it to work with typescript
    * Error: `Uncaught TypeError: Cannot read property 'Observable' of undefined`. Works in plain javascript.
    * Fix:
        * Install type definitions for rxjs `npm install --save-dev @type/rx`
        * Import as `import * as Rx from 'rxjs'`

* Issues with `Rx.DOM.get()`. Error: `The value of the 'Access-Control-Allow-Origin' header in the response must not be the wildcard '*' when the request's credentials mode is 'include'`
    * Fix:
        * [Issue 1732](https://github.com/ReactiveX/rxjs/issues/1732)
        * Provide custom factory for XHR
```javascript
    const settings = {
    crossDomain: true,
    responseType: "json",
    method: "GET",
    createXHR: () => new XMLHttpRequest(),
    url: url
  }
```
## Resources
* [Official Site](http://reactivex.io/rxjs/)
* [Github RX Book](http://xgrommx.github.io/rx-book/index.html)
* [Rx Extensions](https://github.com/Reactive-Extensions)
