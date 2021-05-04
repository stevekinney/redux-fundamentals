---
path: "/creating-a-slice-solution"
title: "Human Slice (Solution)"
order: "7D"
section: "Redux Toolkit"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

```js
import { createSlice, nanoid } from "@reduxjs/toolkit";

const createHuman = (name) => ({
  id: nanoid(),
  name,
  taskIds: [],
});

const initialState = [createHuman("Steve"), createHuman("Wes")];

export const humansSlice = createSlice({
  name: "humans",
  initialState,
  reducers: {
    add: (state, action) => {
      const human = createHuman(action.payload);
      state.push(human);
    },
  },
});
```

Now, we can add that to our store.

```js
import { configureStore } from "@reduxjs/toolkit";
import { humansSlice } from "./HumansSlice";

export const store = configureStore({
  reducer: {
    humans: humansSlice.reducer,
  },
});
```
