## Monomorphism

Fiber nodes (React) and View nodes (Angular) are data structures to represent templates in each framework.

Fiber and View nodes are used a lot when processing changes

> Locating value of an object's property in memory is a complicated process

Every JavaScript object internally inside the VM is also corresponding to a *Shape* (i.e. the *Hidden Class*) object, which describes the layout, which properties the object has and some metadata. For example, if we represent it in JSON:

```
{
  'tag': 'shape',
  'properties': [
    'x': {
        Offset: 0,
        [[Writable]]: true,
        [[Enumerable]]: true,
        [[Configurable]]: true
    },
    'y': {
        Offset: 1,
        [[Writable]]: true,
        [[Enumerable]]: true,
        [[Configurable]]: true
    }
  ]
}
```

Shape works like Class in Java, it acts like blueprint to reduce memory, many similar objects share the same Shape.

If we add some new properties to a object, it creates a new Shape with the property you add, then link the newly created Shape back to the old Shape, which creates Transition Chains.

> The problem with Transition Chains is that if you modify the properties of a object too much, then the Transition Chains will be too long to traverse, which adds much more overhead.

### Inline Cache

Every single JavaScript functions is represented internally by the object called *closure*, where VM caches some information about the function in *feedback vector* (state, shape, prop, offset)

state includes *monomorphic* (monomorphic property access), *polymorphic*, *megamorphic*

- monomorphic: function takes only one type of shapes
- polymorphic: functions takes four types of shapes
- megamorphic: functions takes more than four types of shapes

> monomorphic can be 100 times faster than megamorphic

Hence frameworks enforce the same shape (hidden class) for fiber and view nodes to enable *monomorphic property access*.

## Bit fields

Bit field is an *array of bits*.

```javascript
// different bit flags different state
const bitFiled = 0b00000010
```

React encodes side effects in a bit field, so it doesn't need an array of strings to flag a specific operation.

Pros

- No need to allocate memory for JS objects and shapes
- Simplified garbage collection
- Smaller and contiguous memory usage
- Fast access using a single bitwise operator

## Bloom filters

Bloom filters are bit fields to check wether the element is in the set.

When Bloom Filters give an answer 'NO', the elements is *definitely not* in the set, while 'YES' means the element *could be* in the set with varying probability (because of collisions). So Bloom Filters are used mostly when you want the answer 'NO'.

```javascript
const bitNumber1 = someHashFunc('John')
// for example, bloom filter is a 8-bit bit field
let bloomFilter = 0b00000000
bloomFilter = bloomFilter | bitNumber

// check bits for 'John'
const bitNumber2 = someHashFunc('John')
const isInTheSet = (bloomFilter & bitNumber2) !== 0
```

If hash function introduces collisions then Bloom Filters can't guarantee the presence of the element because there may be another element takes the same bit position.

Angular has hierarchical DI structures, every component has its own injector, so it uses Bloom Filter in DI system to quickly exclude the components that doesn't have the Injector requested.

> Based on [Maxim Koretskyi's talk](https://www.youtube.com/watch?v=_VHNTC67NR8&list=WL&index=94&t=0s)
