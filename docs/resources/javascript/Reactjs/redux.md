# Redux

## Resources
* [Documentation](https://redux.js.org)
* [Getting Started With Redux](https://egghead.io/courses/getting-started-with-redux)
    * [Class Notes](https://github.com/tayiorbeii/egghead.io_redux_course_notes)
* [Build React Applications with Idiomatic Redux](https://egghead.io/courses/building-react-applications-with-idiomatic-redux)
    * [Class Notes](https://github.com/tayiorbeii/egghead.io_idiomatic_redux_course_notes)

## Code Examples.
* Redux Implementation - implement redux from scratch (how it all works together). Only requires React.
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

  return {getState, dispatch, subscribe};
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
const unsub = store.subscribe( () => console.log(store.getState()));

const el = document.getElementById("blog");

const Counter = (props) => {
  const {value, onIncrement, onDecrement} = props;
  return (
    <div>
      <h1>Value: {value}</h1>
      <button className="button large" onClick={onIncrement}>+</button> &nbsp;
      <button className="button large" onClick={onDecrement}>-</button>
      </div>
  );
};

const render = () => ReactDOM.render (
  <Counter value={store.getState()}
          onIncrement = {() => store.dispatch({type: "INCREMENT"})}
          onDecrement = {() => store.dispatch({type: "DECREMENT"})}/>,
  // <AppRoute />,
  el,
);

render();

const renderUnsub = store.subscribe(render);
```
