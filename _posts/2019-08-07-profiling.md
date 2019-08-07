## What is profiling

Profiling is a form of dynamic program analysis that *measures*, for example, the space (memory) or time complexity of a program, the usage of particular instructions, or the frequency and duration of function calls. In mose cases, profiling information serves to aid program optimization. [<sup>1</sup>][1]


## Common Pattern

### Flame Graph

Flame graphs are a visulization of profiled software, allowing the most frequent code-paths to be identified quickly and accurately. They can be generated using open-source [software][2] to create interactive SVGs of flame graph.[<sup>3</sup>][3]

The x-axis of flame graph is *stack profile population*, and the y-axis is *stack depth*, counting from zero at the bottom. Each rectangle represents a stack frame. The wider a frame is, the more often it was present in the stacks.

[The Flame Graph][4]

Ref:

[1]: https://en.wikipedia.org/wiki/Profiling_(computer_programming)
[2]: https://github.com/brendangregg/FlameGraph
[3]: http://www.brendangregg.com/flamegraphs.html
[4]: https://queue.acm.org/detail.cfm?id=2927301