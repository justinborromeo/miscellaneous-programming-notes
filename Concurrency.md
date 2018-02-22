# Concurrency

There are two basic units of execution:
- Processes: have a self-contained execution environment and are allocated memory space.
- Threads: sometimes called lightweight processes, they also provide execution environments but at a lower resource costs.  Threads also exist within processes (every process has at least one).

## Bugs caused by Multi-Threading

Multi-threading can result in a variety of bugs (some of which are hard to detect) as threads can interfere.  Two or more threads accessing the same data can cause unpredictable results.  Examples of such bugs are:
- Memory Consistency Errors: An action performed on one thread is not guaranteed to be visible on another thread unless a happens-before relationship is established.  Examples of actions in Java that create this type of action include Thread.start(), Thread.join(), and synchronization (see section on Synchronization).
- Deadlock: Thread 1 holds the lock to resource A and needs resource B to be unlocked to continue.  Conversely, thread 2 holds the lock to resource B and needs resource A to be unlocked to continue.  Thus, both threads are at a stalemate and are unable to continue causing the program to freeze.
- Starvation: A greedy thread holds the lock to a resource that more frequently-run threads need.  This prevents the more-frequently run threads frome executing.
- Livelock: A thread often acts in response to the action of another thread. If the other thread's action is also a response to the action of another thread, then livelock may result. As with deadlock, livelocked threads are unable to make further progress. However, the threads are not blocked — they are simply too busy responding to each other to resume work. 

## Synchronization in Java

A method tagged as synchronized cannot be run by multiple threads at the same time.  One thread will wait for other to complete.  This establishes a happens-before relationship so that changes performed by one thread are visible to other threads (this isn't guaranteed if the method is non-synchronized).