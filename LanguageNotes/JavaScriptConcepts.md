# JAVASCRIPT CONCEPTS

## React vs. Redux
<img src="ReduxCyclewRails.png" width=550/>
- Redux: yellow, the store, the single-source of truth
- React: green

## Redux Store
- **Store**: central element of Redux's architecture w global state of an app, immutable
  - It 1. updates app's state via reducer 2. broadcasts state to an application's view layer via subscription 3. listens for actions that tell it how and when to change the global state
- ```createStore(reducer, [preloadedState], [enhancer])```
  - reducer (required): reducing function that receives the app's current state and incoming actions, determines how to update the store's state, and returns the next state
- Methods
  - ```getState()```: returns the store's current state.
  - ```dispatch(action)```: passes an action into the store's reducer telling it what information to update
  - ```subscribe(callback)```: registers callbacks to be triggered whenever the store updates (returns function, which when invoked, unsubscribes the callback function from the store)

## Selector
- Selector: functions used to extract and format parts of application state in specific forms
  - Goes in reducer folder

## React/Redux
Provider
- Provider: gives all components access to store, allowing them to read the application state and dispatch actions
- Root component: wraps App component w Provider

connect()
- ```export default connect(mapStateToProps, mapDispatchToProps)(componentName)```
  - Allows passing specific slices of state and action-dispatches to a React component as props
  - Higher-order function
- mapStateToProps: takes state as arg, returns object
  - ownProps: optional 2nd arg, passed like <parentComponent data={'data'}/>
- mapDispatchToProps: takes dispatch, returns object containing functions
