# Threads and Processes

## Threads vs. Processes

There are two basic units of execution:
- Processes: have a self-contained execution environment and are allocated memory space.
- Threads: sometimes called lightweight processes, they also provide execution environments but at a lower resource costs.  Threads also exist within processes (every process has at least one).

## Synchronization

A method tagged as synchronized cannot be run by multiple threads at the same time.  One thread will wait for other to complete.  This establishes a happens-before relationship so that changes performed by one thread are visible to other threads (this isn't guaranteed if the method is non-synchronized).