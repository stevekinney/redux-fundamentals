---
path: "/connect"
title: "Using the Connect API"
order: "4A"
section: "Connecting Redux to React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

In additon to hooks, there is another way to hook up the state in your Redux store and the ability to dispatch actions to your Redux store. In fact, this is the way we did it before hooks hit the scene.

I'll argue that there are still some advantages to this approach.

It separates your state management from your presentational components. This makes it easy to test each independently.

In short, it allows you better separate your concerns. The cost is that it's a bit more verbose. I still really like this approach.

Not only is there no right answer, but also you're likely to see use of `connect()` in many existing code bases. So, regardless of which you decide to prefer, it's definitely worth getting comfortable with both.
