## Scope

How much a framework tries to do for you?

```

         Libraries  vs. Framework

         Primitives vs. Abstractions

         Bazaar     vs. Cathedral

React                                  Angular

<--------------------------------------------->

```

React focuses on providing fundamental lower-level primitives on which custom abstractions, while angular tries to provide complete solutions for users.

### Small Scope 

Pros

- Fewer concepts to get started with
- More flexibility and more userland opportunities -> active ecosystem
- Smaller maintenance surface -> team can focus on exploring new ideas

Cons

- More plumbing work needed when solving inherent complex problems with simple concepts
- Patterns naturally emerge over time and become semi-required knowledge, but often not officially documented
- Ecosystem moving too fast can lead to fragmentation and constant churn

### Large Scope 

Pros

- Most common problems can be solved with built-in abstractions
- Centralized design process ensures consistent and coherent ecosystem

Cons

- Higher upfront learning barrier
- Inflexible if built-in solution doesn't fit use case
- Larger maintenance surface makes introduction fundamental new ideas much more costly

### Progressive Scope (Vue.js)

Pros

- A layered design that allows features to be opted-in in a progressive manner
- Low entry learning barrier
- Documented solutions for common problems

Cons

- Shares the same maintenance surface problem of big scope
- Ecosystem not as diverse as small scope

## Render Mechanism

How a framework allows you to express your UI structure and how it renders stuff

### JSX/Virtual DOM

Pros

- Full *expressiveness* of JavaScript
- Treats the view as *data*
  - Userland possibility of custom usage of view data, e.g. testing & rendering to alternative targets

Cons

- Inherently *expensive* (Standard vdom diffing cost is relative to the total size of the view, rather than the number of nodes that may change)
- *Dynamic* nature of render functions makes it hard to optimize
- Runtime scheduling improves perceived *performance*, but requires a *heavy* runtime

### Template Compilation

Pros

- Can produce more *direct* render instructions with *better raw performance*
- Depends on strategy, may lead to much *lighter* runtime baseline size

Cons

- Users are *constrained* by the template syntax with no escape hatch
- Lighter runtime may come at the cost of more *verbose* output per template
- Runtime compilation cost or a *hard requirement* on a build step

### VDOM + Template

Pros

- Performance: Compilation step produces specially optimized vdom render function
- Expressiveness: Option to skip template and drop down to manually written render functions for full flexibility

## State Mechanism

- Mutable vs. Immutable
- Dependency tracking vs. Dirty Checking
- Reactivity vs. Simulated Reactivity

### Mutable

To be continued...

> Based on [Evan Yu's talk](https://www.youtube.com/watch?v=ANtSWq-zI0s)
