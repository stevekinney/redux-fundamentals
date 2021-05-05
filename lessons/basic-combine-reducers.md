---
path: "/combine-reducers"
title: "Combine Reducers"
order: "2F"
section: "Redux Without React"
description: "Creating Stores and Reducers"
---

Let's stay we have an application where we have some users and we have some tasks. We can assign users and we can assign tasks.

The state might look something like this.

```js
const initialState = {
  users: [
    { id: 1, name: "Steve" },
    { id: 2, name: "Wes" },
  ],
  tasks: [
    { title: "File the TPS reports", assignedTo: 1 },
    { title: "Order more toner for the printer", assignedTo: null },
  ],
};
```

This is still way smaller than a real application, but it's still becoming a pain.

Let's look at what the reducer might look like.

```js
const ADD_USER = "ADD_USER";
const ADD_TASK = "ADD_TASK";

const addTask = (title) => ({ type: ADD_TASK, payload: { title } });
const addUser = (name) => ({ type: ADD_USER, payload: { name } });

const reducer = (state = initialState, action) => {
  if (action.type === ADD_USER) {
    return {
      ...state,
      users: [...state.users, action.payload],
    };
  }

  if (action.type === ADD_TASK) {
    return {
      ...state,
      tasks: [...state.tasks, action.payload],
    };
  }
};

const store = createStore(reducer, initialState);

store.dispatch(addTask("Record the statistics"));
store.dispatch(addUser("Marc"));

console.log(store.getState());
```

This is already getting out of control. It would be nice if we could split out the idea of managing our users and managing our tasks into two separate reducers and just sew everything back up later.

It turns out, we can! We just need to use `combineReducers`.

```js
const users = (state = initialState.users, action) => {
  if (action.type === ADD_USER) {
    return [...state, action.payload];
  }

  return state;
};

const tasks = (state = initialState.tasks, action) => {
  if (action.type === ADD_TASK) {
    return [...state, action.payload];
  }

  return state;
};

const reducer = redux.combineReducers({ users, tasks });

const store = createStore(reducer, initialState);
```

**Fun Fact!**: All actions flow through all of the reducers. So, if you want to update two pieces of state with the same action, you totally can.
