# React Redux Notes
> Notes on Redux as well as its React bindings.

## Redux
Redux is a JavaScript state management library that can be used with any framework (or no framework at all). The core concepts of Redux consist of a single store, actions, and reducers.

Redux has three principles:
 1. **Single Source of Truth**
    - The state of your application is stored in an object tree within a single store.
 2. **State is read-only**
    - The only way to change state is to emit an action - an object describing what happened.
 3. **Changes are made with pure functions**
    - To specify how the state tree is transformed by actions, you write pure reducers.

### Store
The Redux *Store* holds application state, allows access to state via the `getState()` method, allows state to be updated by the `dispatch()` method, and handles registering and unregistering listeners via the `subscribe()` method.

A Redux application can only have a single store, which differs from Flux and MobX which allow you to have multiple stores.

Also, a Redux store is immutable. The state object can only be updated by reducers.

Use the `createStore()` method to create your store. `createStore` accepts 3 arguments:
 - Required: `reducer` (or the result of `combineReducers`)
 - Optional: `preloadedState` - the initial state (useful for hydrating the state from the server)
 - Optional: `enhancer` - any middleware you want to include (such as Redux Dev Tools)
   - Use the `compose` method to include multiple enhancers

Note that Redux will interpret the second argument as an enhancer if it is a function and the third argument is undefined.

The store is not a class instance - it's simply a JavaScript object with a few methods:
 - `getState` - returns the current state tree
 - `dispatch` - dispatches an action to trigger a state change
 - `subscribe` - adds a change listener that is called when an action is dispatched.
   - `subscribe` returns a function that can be saved to a variabled and invoked to unsubscribe the listener.
 - `replaceReducer` - replaces the store's reducer (useful when code splitting and loading reducers dynamically)

```javascript
import { createStore } from 'redux';
import todoApp from './reducers/todoApp';

const store = createStore(
  todoApp,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
);
```

### Actions
Actions are payloads of information that are sent from your application to the Redux store. Actions are sent via the `Store.dispatch()` method. Actions are plain JavaScript objects and must have a `type` property that indicates the type of action being performed.

Actions are returned by Action Creators. An Action Creator is a function that returns an action. If the action is the result of an API call or some other side-effect (asynchronous operation), the Action Creator should return an Async Action (a Promise or thunk). Async Actions are not passed to the reducer immediately, but trigger dispatches once the asynchronous operation has completed. You'll want to use a library like `redux-thunk` (callbacks) or `redux-saga` (generators) when dealing with side-effects.

Action Creators can be bound to the store's `dispatch` method using the `bindActionCreators()` method. The only time you need to do this is when you're passing an action to a component as a prop to a component that isn't aware of Redux or `dispatch`.

Action Types are MACRO_CASE string constants. Conventionally, they are defined in modules that share the same name as the reducer they are used in, i.e., `./reducers/todo.js` and `./actiontypes/todo.js`.

```javascript
// Action Type
const ADD_TODO = 'ADD_TODO';

// Action Creator
const addTodo = (todo) => ({
  type: ADD_TODO,
  text: todo.text,
  completed: todo.completed
});

// Bound Action Creator
// dispatch can be passed as a prop or injected by react-redux
const boundAddTodo = bindActionCreators(addTodo, dispatch);
```

### Reducers
Reducers are pure functions that take previous state and an action as arguments and return the updated state. They are called reducers because they are the type of function you would pass to the JavaScript array `reduce` method.

Reducers must remain pure, which means their arguments should never be mutated, they should never trigger side-effects (like make an API call), and you should never call an impure function inside them (like `Date.now()`, `Math.random()`, or `uuid()`).

Most Redux Reducer examples use `switch` statements, but you do not have to follow that pattern (although it does look better than a bunch of chained `if`/`else if`/`else` statements). Typically you'll want to return the state object in your `default` or `else` block (i.e., if your action type was not recognized).

```javascript
// The individual todo object
const todo = (state, action) => {
  switch (action.type) {
    case ADD_TODO:
      return {
        text: action.text,
        completed: false
      };
    default:
      return state;
  }
};

// The array of todos
// Note the use of ES6 default argument syntax
const todos = (state = [], action) => {
  switch (action.type) {
    case ADD_TODO:
      return [
        ...state,
        todo(state, action)
      ];
    default:
      return state;
  }
};
```
