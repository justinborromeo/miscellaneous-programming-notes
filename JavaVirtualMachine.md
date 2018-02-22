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
    - JIT Compiler: Eliminates need for certains methods to be reinterpreted every time they are run (see section on Hotspot Optimization).  Instead, it is compiled to native code, which executes faster.
4. Native Method Interface: Interacts with the Native Method Libraries and provides the Native Libraries required for the Execution Engine.
5. Native Method Libraries: A collection of the Native Libraries which are required for the Execution Engine.

## The Java Memory Model

### Stack
- Holds references to heap objects and stores primitives
- Once a method is complete, the stack frame for the method (which contains the local variables) is popped off the stack
- 1 stack/thread, therefore thread-safe

### Heap
- Only one heap per JVM process (multiple threads use the heap at the same time, so not thread-safe)
- Stack variables point to objects on the heap
- Objects on the heap can point to other objects on the heap
- Much larger than stack in terms of memory size.

### Stack-Heap References
- Strong: Object on heap is never garbage collected if a strong reference is pointing to it or if it is reachable from the stack through a chain of strong references
- Weak: Will not survive a garbage collection 
- Soft: Cleaned by garbage collection if the application is running out of memory

### Strings (Objects in Java)
- Identical string literals are stored in the same heap object in the string pool
```Java
String one = "Hello";
String two = "Hello";
//one == two will return true as they both have the same heap address
```
- Computed strings are not stored in the same heap object
```Java
String one = "297";
String two = new Integer(297).toString()
//one != two as they have different addresses on the heap
```
- A computed string can be added to the string pool using the String object's .intern() method

## Generational Garbage Collection

## Hotspot Optimization