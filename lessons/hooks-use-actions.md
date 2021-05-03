---
path: "/use-actions"
title: "Binding Actions"
order: "3H"
section: "Hooking It Up With React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

We saw in our introduction that we can create functions that implicitely know about—or are _bound_ to—dispatch.

At a simple version of this might look as follows:

```js
const actions = bindActionCreators({ increment, decrement, set }, dispatch);
```

And now we could put them into the component.

```js
<button onClick={() => actions.increment()}>Increment</button>
<button onClick={() => actions.set(0)}>Reset</button>
<button onClick={() => actions.decrement()}>Decrement</button>
```

You could even create a hook if you wanted to do this on the regular.

In a new file called `set-actions.js`:

```js
import { bindActionCreators } from "redux";
import { useDispatch } from "react-redux";
import { useMemo } from "react";

export function useActions(actions) {
  const dispatch = useDispatch();
  return useMemo(() => {
    return bindActionCreators(actions, dispatch);
  }, [actions, dispatch]);
}
```

And now we can use this whenever.

```js
const actions = useActions({ increment, decrement, set });
```

[A similar function][use-actions] was originally included in an alpha of React Redux, but was ultimately removed for [reasons][].

[use-actions]: https://react-redux.js.org/api/hooks#recipe-useactions
[reasons]: https://github.com/reduxjs/react-redux/issues/1252#issuecomment-488160930
