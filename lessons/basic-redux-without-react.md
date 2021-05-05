---
path: "/redux-api"
title: "Redux's API"
order: "2A"
section: "Redux Without React"
description: "Get comfortable with Redux by itself"
---

Let's start by getting a sense of the lay of the land. Redux, for all of its power, has a relatively small API footprint.

- `applyMiddleware`
- `bindActionCreators`
- `combineReducers`
- `compose`
- `createStore`

Yup, just five functions. We'll discuss each of this in due time. We'll start with one of the simple utility methods that come along with Redux.

## `compose`

If we want to split hairs. It's actually less than that. `compose()` isn't exactly Redux-specific. It's just a helper function. `compose` takes a series of functions as arguments and returns a new function that applies each those functions from right-to-left (or, from last-to-first if you're like me and have trouble discerning right from left).

Let's say that we had a bunch of functions that each take a string and return a modified string.

```js
const makeLouder = (string) => string.toUpperCase();
const repeatThreeTimes = (string) => string.repeat(3);
const embolden = (string) => string.bold();
```

(Yea, I just learned that some of those methods exist too.)

We _could_ call them all like this:

```js
embolden(repeatThreeTimes(makeLouder("hello")));
```

But, what if I wanted to pass this combined function around as an argument to another function or method? I'd have to do something like this:

```js
const makeLouderAndBoldAndRepeatThreeTimes = (string) =>
  embolden(repeatThreeTimes(makeLouder(string)));
```

This is tedious. `compose` gives us a simple way to _compose_ functions out of other functions.

```ts
const makeLouderAndBoldAndRepeatThreeTimes = redux.compose(
  embolden,
  repeatThreeTimes,
  makeLouder
);
```

You'll see a similiar utility in other libraries like [Lodash](https://lodash.com/docs/4.17.15#flow) and [Ramda](https://ramdajs.com/docs/#compose).

This is used as a helper when creating enhancers, which we'll talk about in the a more advanced workshop. For now, I'm just fulfilling my promises of demystifying the core API.
