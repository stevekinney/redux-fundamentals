---
path: "/create-async-thunk"
title: "Creating Async Thunks in Redux Toolkit"
order: "8A"
section: "Asynchronous Actions"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

A thunk is a fancy way of saying you're going to dispatch a function that is eventually going to dispatch an action.

Redux toolkit comes with a nice way of seeing that play out.

```js
const ENDPOINT = "https://star-wars-characters.glitch.me/api/search/";

export const fetchCharactersFromAPI = createAsyncThunk(
  "characters/fetchCharacters",
  async (searchTerm) => {
    const response = await fetch(
      ENDPOINT + searchTerm.toLowerCase()
    ).then((response) => response.json());
    return response.results;
  }
);
```

In `extraReducers` we add the following:

```js
export const charactersSlice = createSlice({
  name: "characters",
  initialState,
  extraReducers: {
    [fetchCharactersFromAPI.fulfilled]: (state, action) => {
      state.data = action.payload;
    },
  },
});
```

## Exercise

Can you listen for `fetchCharactersFromAPI.pending` and turn the `loading` on and then turn it off then the promise is fulfilled?

<iframe src="https://codesandbox.io/embed/5x0j0?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="chores-redux"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

You can see a solution [here](https://github.com/stevekinney/starwars-redux/commit/92e906c8fa1895381a0150c028eca3cac0a144c7).
