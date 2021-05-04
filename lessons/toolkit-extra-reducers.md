---
path: "/extra-reducers"
title: "Extra Reducers"
order: "7G"
section: "Redux Toolkit"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Okay, we want to get those dropdowns working, right? It's pretty easy to assign a task to a user in the `tasksSlice`.

```js
export const tasksSlice = createSlice({
  name: "tasks",
  initialState,
  reducers: {
    assignToUser: (state, action) => {
      const task = state.find((task) => task.id === action.payload.taskId);
      task.assignedTo = action.payload.humanId;
    },
  },
});
```

But, how do we update the `humanSlice` in order to pop the task ID on the array? If this was a regular reducer, it wouldn't be so bad. We're going to need something.

Let's look at it in pseudocode first…

```js
export const humansSlice = createSlice({
  // …
  extraReducers: (builder) => {
    builder.addCase(tasksSlice.actions.assignToUser, (state, action) => {
      // Do stuff with the state of your humansSlice
      // and the action that came in from the tasksSlice.
    });
  },
});
```

Here it is in practice. The only trickiness here is that we're looking to add a task to one human. That's easy, but we also have to iterate through the other humans and remove. But, that's a JavaScript problem—not a Redux problem.

```js
export const humansSlice = createSlice({
  // …
  extraReducers: (builder) => {
    builder.addCase(tasksSlice.actions.assignToUser, (state, action) => {
      for (const human of state) {
        if (human.id === action.payload.humanId) {
          human.taskIds.push(action.payload.taskId);
        } else {
          human.taskIds = human.taskIds.filter(
            (id) => id !== action.payload.taskId
          );
        }
      }
    });
  },
});
```
