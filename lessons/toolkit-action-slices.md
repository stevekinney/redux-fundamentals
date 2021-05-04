---
path: "/slice-actions"
title: "Slice Actions"
order: "7E"
section: "Redux Toolkit"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

The slice creates action creators based on the name of keys in the reducer. Let's dispatch the action from the slice in `CreateHuman`

```js
dispatch(humansSlice.actions.add(name));
```

That's it. No need to import a bunch of constants and action creators.

## Exercise

Okay, it's your turn—add it to `CreateTask`.
