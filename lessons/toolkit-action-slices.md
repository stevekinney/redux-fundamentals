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

<iframe src="https://codesandbox.io/embed/sruo9?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="chores-redux"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
