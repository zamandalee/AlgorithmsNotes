# Frontend (React) Testing

## Setup
Terminal
- npm install --save-dev jest
- npm install --save-dev redux-mock-store: sample testing store

package.json
- "scripts": { "test": "jest" }

.babelrc
- { "presets": [ "es2015", "react" ] }

## Tests
__tests__/[file_to_test]-test.js
- tests here

```js
// bench_actions-test.js

// make a mock API call and engineer a response
ApiUtil.fetchBenches = jest.fn( () => {
  return Promise.resolve(testBenches); //create a Promise
});

let store = mockStore({ benches: {} });
return store.dispatch(actions.fetchBenches()).then( () => {
  // jest func mockStore.getActions to array of actions called
  expect(store.getActions()).toEqual(expectedActions);
});
```
