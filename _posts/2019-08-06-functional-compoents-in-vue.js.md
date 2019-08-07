## What is functional components

- Can't have its own data, computed properties, watchers, lifecycle events, or methods.
- Can't have a template, unless that is precompiled template from a single-file component. That's why we used a render function above.
- Can be passed, things like props, attributes, events, and slots.
- Returns a Vnodes or an array of VNodes from a render function. Unlike a normal component that has to have a single root Vnodes, it can return an array of VNodes.

## Why choose functional components

Functional components are cheaper than normal components because they don't have a Vue instance associated with them, they just create an extra VNode which means less JavaScript executed and less memory allocated.

## Use Case

1. Cheap leaf components that can be reused without the cost of stateful instantiation component
2. Functional wrapper components (e.g, [`router-view`])

##  Example

[`router-view`]: https://github.com/vuejs/vue-router/blob/dev/src/components/view.js#L5