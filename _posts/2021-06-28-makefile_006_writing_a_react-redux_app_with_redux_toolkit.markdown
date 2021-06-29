---
layout: post
title:      "Makefile 006: Writing a React-Redux App with Redux Toolkit"
date:       2021-06-29 03:36:54 +0000
permalink:  makefile_006_writing_a_react-redux_app_with_redux_toolkit
---


As the saying goes, there's a first time for everything. For my final project as a student with Flatiron School, I was tasked with writing an app using the React Javascript framework and the Redux state management library. Though it wasn't part of our curriculum, I came across [Redux Toolkit](https://redux-toolkit.js.org/) from the Redux core team and wanted to try it out. As they say on their site, it's "The official, opinionated, batteries-included toolset for efficient Redux development."

Redux is a bit like a client-side database. It allows access to data in-browser to manipulate application state. It includes:

* A store: A collection of objects or arrays holding state data relevant to the operation of the app.

* Actions: Objects that contain instructions for changing data in the store, consisting of a type (the kind of change you want to make) and a payload (the information for the change).

* Reducers: A.K.A. "case reducers," functions that perform changes based on the actions dispatched to them.

While the basic functionality of Redux is the same, whether using the traditional form or the newer Redux Toolkit, the implementation is quite different, with the Toolkit aiming to simplify and automate how Redux is used. To illustrate, I'll use examples from my app, [Restauranter](https://github.com/ronsala/restauranter-frontend), a restaurant-management web app.

## Store

### Traditional Redux

Uses a `createStore` function. This function also sets up the Redux Devtools, which is useful for seeing into the app's state. To use more than one reducer, a `combineReducers` function is employed.

```javascript
import { combineReducers } from 'redux';
import { createStore } from 'redux';

[Import reducers.]

const rootReducer = combineReducers({
    items: itemsReducer,
    menus: menusReducer,
    orderitems: orderitemsReducer,
    orders: ordersReducer,
    restaurants: restaurantsReducer,
    sections: sectionsReducer,
    users: usersReducer, 
});

const store = createStore(
  rootReducer,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
);
```

## Redux Toolkit

Uses a `configureStore` function.  Redux Devtools is set up automatically. To use more than one reducer, they can be listed as part of a `reducer` object.

```javascript
export const store = configureStore({
  reducer: {
    items: itemsReducer,
    menus: menusReducer,
    orderitems: orderitemsReducer,
    orders: ordersReducer,
    restaurants: restaurantsReducer,
    sections: sectionsReducer,
    users: usersReducer,
  },
});
```

## Actions

### Traditional Redux

Actions are set up manually as objects. For example,

```javascript
const addItemAction = {
  type: ADD_ITEM,
  payload: 'French Onion Soup'
}
```

### Redux Toolkit

Actions can be created through the `createEntityAdapter` function in a slice function, which administers a "slice" of state, e.g. Items, Orders, Sections, etc.

```javascript
import { 
  createSlice,
  createEntityAdapter,
} from '@reduxjs/toolkit'

const itemsAdapter = createEntityAdapter({
  selectId: (item) => item.id
})

export const itemsSlice = createSlice({
  name: 'item',
  initialState: itemsAdapter.getInitialState({
    status: 'idle'
  }),
  reducers: { 
    addOneItem: itemsAdapter.addOne, 
  }
})
```

## Reducers

### Traditional Redux

Reducers are created in the form of a switch statement. Care must be paid to adhere to functional programming principles by not mutating the state but instead returning a new state.

```javascript
export default function itemReducer(
  state = {
    items: []
  },
  action
) {
  switch (action.type) {
    case 'ADD_ITEM': {
      return Object.assign({}, state, {
        items: state.todos.concat({
          name: action.name,
          desc: action.desc,
          price: action.price,
          menu_id: action.menu_id
        })
      })
    }
 
    default:
      return state;
  }
}
```

### Redux Toolkit

Uses the Immer library, which returns a new state automatically. For instance, we can set up an asynchronous fetch of an item and add it to the store through the itemsSlice function in an `extraReducers` section that processes the action on a successful response.

```javascript
    [postItem.fulfilled]: (state, action) => {
      state.status = 'succeeded'
      itemsAdapter.addOne(state, action.payload.data)
    },
```

Redux Toolkit takes some getting used to but provides powerful functionality with minimal lines of code. You might want to consider it for your next project.

The content of your blog post goes here.
