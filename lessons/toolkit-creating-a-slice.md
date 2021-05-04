---
path: "/creating-a-slice"
title: "Creating a Slice of State"
order: "7B"
section: "Redux Toolkit"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Create the store in `store/index.js`:

```js
import { configureStore } from "@reduxjs/toolkit";

export const store = configureStore({
  reducer: (state) => state,
});
```

That's a dummy reducer for now. Redux Toolkit uses something called "slices" for managing state. Don't worry. This isn't anything new, it's just an abstraction over everything we've seen so far in this workshop.

Okay, let's scope out the features in our application.

- We're going to have humans that we can add to the household.
- We'll have a list of all of those humans and if they decide to change their name, we'll allow for that.
- We're going to be able to add tasks that need to get done.
- We'll have a list of all of the tasks currently in the application.
- We'll be able to mark a task as done or not.
- We'll be able to assign a task to a human.
- We'll see all of the tasks sorted by the human their assigned to.

## Creating a Tasks Slice

Okay, so what would our first tasks slice look like?

```js
import { createSlice, nanoid } from "@reduxjs/toolkit";

const createTask = (title) => ({
  id: nanoid(),
  title,
  complete: false,
  assignedTo: "",
});

const initialState = [
  createTask("Order more energy drinks"),
  createTask("Water the plants"),
];

export const tasksSlice = createSlice({
  name: "tasks",
  initialState,
  reducers: {
    add: (state, action) => {
      const task = createTask(action.payload);
      state.push(task);
    },
  },
});
```

And now we can add it to the store.

```js
import { configureStore } from "@reduxjs/toolkit";
import { tasksSlice } from "./TasksSlice";

export const store = configureStore({
  reducer: {
    tasks: tasksSlice.reducer,
  },
});
```

Boom. Now go check out the Redux Developer Tools—yes, they're already wired up—and see that we have our task loaded into state.
