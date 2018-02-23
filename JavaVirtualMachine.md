# The Java Virtual Machine

The JVM is an abstract runtime environment in which Java bytecode can be executed.

## Overall JVM Architecture

1. Class Loader: Loads, links, and initializes the class file when a class is first referred to at runtime
2. JVM Memory
    - Method area: All class-level data is stored here, including static variables.  This area is not thread-safe as it is a shared resource between threads.
    - Heap area: Stores objects and corresponding instance variables and arrays.  This area is not thread-safe as it is a shared resource between threads.
    - Stack area: For every method call, a stack frame entry is made in the thread's stack.  Each stack frame stores local variables in an array, has an operand stack for intermediate operations, and stores frame data, which includes data about catch-statements.
    - PC Registers: Stores address of the currently executing instruction.
    - Native method stack: Holds native method info.
3. Execution Engine
    - Interpreter: Interprets and executes Java bytecode (a form of instruction set designed for efficient execution by a software interpreter)
    - JIT (Just-in-Time) Compiler: Eliminates need for certains methods to be reinterpreted every time they are run (see section on Hotspot Optimization).  Instead, it is compiled to native code, which executes faster.
4. Native Method Interface: Interacts with the Native Method Libraries and provides the Native Libraries required for the Execution Engine.
5. Native Method Libraries: A collection of the Native Libraries which are required for the Execution Engine.

## The Java Memory Model

### Stack
- Holds references to heap objects and stores primitives.
- Once a method is complete, the stack frame for the method (which contains the local variables) is popped off the stack.
- 1 stack/thread, therefore thread-safe.

### Heap
- Only one heap per JVM process (multiple threads use the heap at the same time, so not thread-safe).
- Stack variables point to objects on the heap.
- Objects on the heap can point to other objects on the heap.
- Much larger than stack in terms of memory size.

### Stack-Heap References
- Strong: Object on heap is never garbage collected if a strong reference is pointing to it or if it is reachable from the stack through a chain of strong references.
- Weak: Will not survive a garbage collection.
- Soft: Cleaned by garbage collection if the application is running out of memory.

### Strings (Objects in Java)
- Identical string literals are stored in the same heap object in the string pool.
```Java
String one = "Hello";
String two = "Hello";
//one == two will return true as they both have the same heap address
```
- Computed strings are not stored in the same heap object.
```Java
String one = "297";
String two = new Integer(297).toString()
//one != two as they have different addresses on the heap
```
- A computed string can be added to the string pool using the String object's .intern() method.

## Generational Garbage Collection
- Garbage collection is generally inefficient because the entire program must halt.
- The basis of garbage collection is the mark-and-sweep process.  This process looks for objects on the heap that are strongly (or softly) referenced by an item on the stack.  "Living" objects are marked; unmarked objects are deallocated upon sweeping.
- If an object survives a mark-and-sweep a certain number of times (the threshold value depends on JVM implementation), it is moved to an "older" part of the heap".  Older parts of the heap are garbage collected less often (it is assumed that the more mark-and-sweeps an object survives, the longer it will persist).  This decreases the average garbage collection time for every iteration.
- Types:
    - Serial GC: Single-threaded
    - Parallel GC: Multi-threaded
    - Mostly Concurrent GC: Runs concurrently to application (there is a small pause)
        - Garbage First: High throughput with a reasonable pause
        - Concurrent Mark Sweep: Minimum pause time

## Hotspot Optimization
- Hotspot optimization occurs in the Java Hotspot VM
- Two main features:
    - Adaptive Optimization: The JVM determines which methods (in interpreted bytecode) are "hotspots" based on how often they are executed.  Hotspots are then compiled to significantly faster native code (the method's interpreted bytecode can still be called during compilation and optimization).  The hotspot method of optimization is a much faster JIT compilation and results in better-optimized code as the JVM has more time to perform optimizations than traditional JIT methods.
    - Adaptive Inlining: Optimizers don't work as well when crossing method boundaries since they have to focus on code between method invocations.  The solution to this issue is inlining: copying the invoked method's body into the body of the invoking method.  Inlining is hard to do in OOP languages (such as Java and C++) as multiple implementations of a method have to be chosen at runtime.  As a result,one way of inlining is to inline every possible implementation of method...however, this is memory-inefficient.  The Hotspot VM inlines  "hotspot" methods at runtime before JIT compilation, greatly reducing the number of methods that need to be inlined. 