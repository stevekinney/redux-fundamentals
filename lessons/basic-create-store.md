---
path: "/create-store"
title: "Redux Stores and Reducers"
order: "2B"
section: "Redux Without React"
description: "Creating Stores and Reducers"
---

So, now for those of you keeping tract at home, we're now really talking about four functions. That's write, we've already covered about 80% of the API and we're just getting started.

Covering `compose()` first was kind of cheating. It's not really super important to understanding Redux. But, we'll take our small wins when we can get them, right?

Redux is a friendly state management library. In this industry, we tend to call the place where we keep our state the "store." Redux's `createStore()` method will … create … a … store.

One does not just create a Redux store, however.

```js
let store = redux.createStore();
```

This will blow up, but at least we get a helpful error message.

> Error: Expected the reducer to be a function.

So, there are two things to take away from this: we need to provide an argument that is a reducer and a reducer is a function. What is a reducer?

Let's stop for a minute and talk about Redux at a high level. We have the state of our application. We have things that happen (e.g. user actions, WebSocket messages, etc.). When a thing happens, what effect does that have on the state of our application?

Well, friends, a reducer is a function where the first argument is the current state of the world and the second is something that happened. Somewhere inside of the function, we figure out what the new state of the world ought to be based on whatever happened.

That's the job of the reducer. It looks at the new thing that happened and it looks at the current state of the world and returns a new state of the world.

Here's the crazy thing: it's just a function. It takes two arguments: the thing that just happened and the current (soon to be previous) state of the world. It returns one thing: the new state of the world.

To get things started, we're going to make a simple calculator. The state of the world will be an object that stores the current result, which will default to zero.

```ts
type ApplicationState = {};
type Action: { type: string, [key: string]: any }

type Reducer = (state: ApplicationState, action: Action) => ApplicationState
```

So, let's start with a super simple example:

```js
const initialState = { value: 0 };

const reducer = (state = initialState, action) => {
  return state;
};
```

An action is just an object. The only requirement is that is has a `type` property. Sure, something happened, but what type of thing happened?

```js
const incrementAction = { type: "INCREMENT" };
```

It's convention to use SNAKE_CASE for our actions. I don't know why and frankly, I don't make the rules around here. You can ignore this if you want to at your own peril.

Let's say an increment action comes in. Well, we should probably increment the value, right?

```js
const initialState = { value: 0 };

const reducer = (state = initialState, action) => {
  if (action.type === "INCREMENT") {
    return { value: state.value + 1 };
  }

  return state;
};
```

Alright, there are a few things here. You'll notice that we're creating a new object rather than mutating the existing one. This is helpful because it allows anything depending on this state to figure out that we have a new state of the world. We also want to make sure we return the existing state in the event that an action we don't care about comes through the reducer.

We can make this a little bit better too:

```js
const initialState = { value: 0 };

const INCREMENT = "INCREMENT";

const incrementAction = { type: INCREMENT };

const reducer = (state = initialState, action) => {
  if (action.type === INCREMENT) {
    return { value: state.value + 1 };
  }

  return state;
};
```

You'll notice we made a constant called `INCREMENT`. The main that we took this approach is because we needed to make sure that we didn't accidentally mispell the action type—either when we created the action or in the reducer. At least now, our code will blow up. This sure beats silently failing.

We'll also typically use functions to create our actions since they might need more information.

```js
const initialState = { value: 0 };

const INCREMENT = "INCREMENT";
const ADD = "ADD";

const increment = () => {
  type: INCREMENT;
};
const add = (number) => ({ type: ADD, payload: number });

const reducer = (state = initialState, action) => {
  if (action.type === INCREMENT) {
    return { value: state.value + 1 };
  }

  if (action.type === ADD) {
    return { value: state.value + action.payload };
  }

  return state;
};
```

Calling it a `payload` is also just a convention. You'll probably notice that nothing in the last few code samples have literally nothing to do with Redux. It's all just JavaScript.

We follow the conventions because we want our colleagues to like us.

But, we have a reducer now, so that's nice.

```js
const store = redux.createStore(reducer);
```

We now have an initial state of the world and some logic about how it should change in the event that a limited set of things happen.
