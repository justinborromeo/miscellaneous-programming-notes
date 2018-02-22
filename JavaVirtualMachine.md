# The Java Virtual Machine

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


## Generational Garbage Collection

## Hotspot Optimization