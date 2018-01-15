# React Redux Notes
> Notes on Redux as well as its React bindings.

## Redux
Redux is a JavaScript state management library that can be used with any framework (or no framework
at all). The core concepts of Redux consist of a single store, actions, and reducers.

Redux has three principles:
 1. **Single Source of Truth**
    - The state of your application is stored in an object tree within a single store.
 2. **State is read-only**
    - The only way to change state is to emit an action - an object describing what happened.
 3. **Changes are made with pure functions**
    - To specify how the state tree is transformed by actions, you write pure reducers.

### Store
The Redux store holds application state, allows access to state via the `getState` method,
allows state to be updated by the `dispatch` method, and handles registering and unregistering
listeners via the `subscribe` method.

A Redux application can only have a single store, which differs from Flux and MobX which allow you
to have multiple stores.

Also, a Redux store is immutable. The state object can only be updated by reducers.

Use the `createStore` method to create your store. `createStore` accepts 3 arguments:
 - Required: `reducer` (or the result of `combineReducers`)
 - Optional: `preloadedState` - the initial state (useful for hydrating the state from the server or `localStorage`)
 - Optional: `enhancer` - any middleware you want to include (such as Redux Dev Tools)
   - Use the `compose` method to include multiple enhancers

Note that Redux will interpret the second argument as an enhancer if it is a function and the third
argument is undefined.

The store is not a class instance - it's simply a JavaScript object with a few methods:
 - `getState` - returns the current state tree
 - `dispatch` - dispatches an action to trigger a state change
 - `subscribe` - adds a change listener that is called when an action is dispatched.
   - `subscribe` returns a function that can be saved to a variable and invoked to unsubscribe the listener.
 - `replaceReducer` - replaces the store's reducer (useful when code splitting and loading reducers dynamically)

A basic store would look like this:

```javascript
const store = createStore(
  reducers,
  // initialState
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
);
```

You can also conditionally add enhancers to the store by creating a `configureStore` function that
returns a call to `createStore`. This example uses the `composeWithDevTools` method from
`redux-devtools-extension` to inject the Redux Devtools Extension into our middleware list.

```javascript
const configureStore = () => {
  let middleware = [routerMiddleware(history), reduxThunk];
  
  if (process.env.NODE_ENV !== 'production') {
    middleware.push(reduxLogger);
  }
  
  return createStore(
    reducers,
    // initialState,
    composeWithDevTools(applyMiddleware(...middleware))
  );
}
```

### State Tree
In a Redux application, the state of the entire application is stored in a single tree. The shape of
the state tree comes from the root reducer passed to `createStore`. For example if your root reducer
looked like this:

```javascript
const reducers = combineReducers({
  todos,
  router: routerReducer,
  form: formReducer
});
```

Your state tree would look like this:

```javascript
{
  todos: {},
  router: {},
  form: {}
}
```

### Actions
Actions are payloads of information that are sent from your application to the Redux store. Actions
are sent via the `store.dispatch` method. Actions are plain JavaScript objects and must have a
`type` property that indicates the type of action being performed.

Actions are returned by Action Creators. An Action Creator is a function that returns an action. If
the action is the result of an API call or some other side-effect (asynchronous operation), the
Action Creator should return an Async Action (a Promise or thunk). Async Actions are not passed to
the reducer immediately, but trigger dispatches once the asynchronous operation has completed.
You'll want to use a library like `redux-thunk` (callbacks) or `redux-saga` (generators) when
dealing with side-effects.

Action Creators can be bound to the store's `dispatch` method using the `bindActionCreators`
method. The only time you need to do this is when you're passing an action to a component as a prop
to a component that isn't aware of Redux or `dispatch`.

Action Types are MACRO_CASE string constants. Conventionally, they are defined in modules that share
the same name as the reducer they are used in, i.e., `./reducers/todo.js` and
`./actions/todo.js`.

```javascript
// Action Type
const ADD_TODO = 'ADD_TODO';

// Action Creator
const addTodo = (todo) => ({
  type: ADD_TODO,
  text: todo.text,
  completed: todo.completed
});
```

### Thunks
A thunk is a function returned within another function. Normally, action creators are functions that
return a plain action object. When working with asynchronous code (i.e., an API call), you can write
actions that return a function. To enable Redux to work with such actions, you need to use the
`redux-thunk` middleware package.

```javascript
const loadTodos = (dispatch) => {
  return async (dispatch) => {
    try {
      const response = await axios.get('/todos');
      
      // dispatch could also have called an action creator
      return dispatch({
        type: GET_TODOS_SUCCESS,
        filter,
        response
      });
    } catch (error) {
      return dispatch({
        type: GET_TODOS_ERROR,
        filter,
        message: error.message
      });
    }
  }
};
```

### Reducers
Reducers are pure functions that take previous state and an action as arguments and return the
updated state. They are called reducers because they are the type of function you would pass to the
JavaScript array `reduce` method.

Reducers must remain pure, which means their arguments should never be mutated, they should never
trigger side-effects (like make an API call).

Most Redux Reducer examples use `switch` statements, but you do not have to follow that pattern
(although it does look better than a bunch of chained `if`/`else if`/`else` statements). Typically
you'll want to return the state object in your `default` or `else` block (i.e., if your action type
was not recognized).

Conventionally, reducers are named after the state properties they manage. Your app can have a
single reducer; although it is more common to split your reducers up to individually manage a
state property. When using multiple reducers, use the `combineReducers` method to compose your
reducers into a single reducing function. The resulting reducer will call each child reducer and
concatenate their results into a single state object. `combineReducers` is passed an object with
each reducer as a property, and thus, it is popular to use ES6 property shorthand syntax, e.g.,
`combineReducers({ todos, filter })`.

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

### Selectors
Selectors are functions that compute data derived from the state. For example, a selector is used to
filter the list of todos based on the current visibility filter (all, active, or completed).

Using selectors allows Redux to store the simplest state tree possible, and also prevents you from
doing computations in your components, which should just render the data they receive as props.

Conventionally, selectors are prefixed with the word`get`.

```javascript
const getVisibleTodos = (todos, filter) => {
  switch (filter) {
    case 'SHOW_ALL':
      return todos;
    case 'SHOW_ACTIVE':
      return todos.filter((todo) => !todo.completed);
    case 'SHOW_COMPLETED':
      return todos.filter((todo) => todo.completed);
    default:
      return todos;
  }
};
```

The downside to this approach is that `getVisibleTodos` is calculated every time the component
updates - even if the todos array or filter string doesn't change. This is where the `reselect`
library comes in.

Reselect allows you to create *memoized* selectors. Memoization is the process of storing the
results of a function call in memory. When the function is called again and passed the same input,
the cached result is returned instead of invoking the function again.

To memoize the `getVisibleTodos` function, use Reselect's `createSelector` method. `createSelector`
takes an array of "input selectors" as its first argument, followed by a transformation function.

```javascript
// Input selectors
const getVisibilityFilter = (state) => state.visibilityFilter;
const getTodos = (state) => state.todos;

// Memoized selector
const getVisibleTodos = createSelector(
  [getVisibilityFilter, getTodos],
  (visibilityFilter, todos) => {
    switch (filter) {
      case 'SHOW_ALL':
        return todos;
      case 'SHOW_ACTIVE':
        return todos.filter((todo) => !todo.completed);
      case 'SHOW_COMPLETED':
        return todos.filter((todo) => todo.completed);
      default:
        return todos;
    }
  }
);
```

Reselect selectors are typically stored in a `selectors` folder.

### Scaffolding
While Redux is completely unopinionated, the examples in the docs use this folder structure:

```bash
src
├── actions    # action creators and optionally action types
├── components # "dumb" components that are unaware of Redux
├── containers # "smart" components connected to Redux
├── reducers   # file names should correspond to state key
├── selectors  # can be exported from a single index.js file
└── store      # invoke createStore here
```

*Note: Action Creators and Action Types can be defined in `actions/index.js` and exported
individually as named exports. Reducers are typically defined in individual files, with
`combineReducers` as the default export in `reducers/index.js`.*

## React Redux
React Redux is the official React binding for Redux, developed by the
[React Community](https://github.com/reactjs). React Redux embraces the idea of separating
presentational ("dumb") components and container components ("smart").

Presentational components are not connected to Redux and receive data and functions as props.

Container components are "generated" by the React Redux `connect` function, which subscribes them to
the Redux store. These components also dispatch Redux actions.

### Provider
The `<Provider>` component provides access to the Redux store to all connected components. The
Provider component is the highest-level component in a React Redux app. It takes the store as a
prop.

```javascript
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

### Connect
The `connect` function is a higher-order function that wraps a component and returns a
higher-order component. This higher-order component is now connected to the Redux store.

Connect accepts the following arguments:
 - `mapStateToProps` 
 - `mapDispatchToProps`
 - `mergeProps`
 - `options`

```javascript
connect(mapStateToProps, mapDispatchToProps, mergeProps, options)(App);
```

Connect can also be used as a class decorator:

```javascript
@connect(arguments)
class App extends Component {}
```

### `mapStateToProps`
A function that subscribes the component to the Redux store, and fired every time the store updates.
The return value must be a plain object, which will be merged into the component's props.

The first argument as always the state. Optionally, a second argument may be passed which gives
access to the component's own props.

```javascript
const mapStateToProps = (state) => ({
  todos: getVisibleTodos(state)
});
```

### `mapDispatchToProps`
Can be an object of action creators, or a function that returns such an object.

If it is an object, each function inside it will be wrapped in a dispatch call, and merged into the
component's props.

If it is a function, it will be given `dispatch` as its first argument, and optionally `ownProps` as
its second.

If no `mapDispatchToProps` argument is passed to `connect`, the `dispatch` method will be passed to
the component's props by default.

```javascript
const mapDispatchToProps = (dispatch) => ({
  // Using object method shorthand notation
  dispatchAddTodo (text) {
    dispatch(addTodo(text));
  }
});
```

### `mergeProps`
A function that takes `stateProps`, `dispatchProps`, and `ownProps` as arguments and returns a plain
object to be passed as props to the component. `connect` will pass to it the results of
`mapStateToProps` and `mapDispatchToProps`.

In most cases, you will not need to use `mergeProps`.

### `options`
Finally, `connect` can be passed an optional options object to customize the behavior of the
connected component. The various properties are defined
[here](https://github.com/reactjs/react-redux/blob/master/docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options).

## Redux Middleware
Redux can be infinitely enhanced by its massive ecosystem of middleware, like the already mentioned
Redux Thunk and Redux Dev Tools.

Middleware in Redux is similar to middleware in Express, in that is composable in a chain. Redux
middleware provides an extension between dispatching an action, and the moment it reaches the
reducer.

### Redux Dev Tools
