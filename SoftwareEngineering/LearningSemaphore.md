# The Little Book of Semaphores 

## Chapter 1 Introduction

* In common use, “synchronization” means making two things happen at the same time. 
* In computer systems, synchronization is a little more general; it refers to ==**relationships**== among events—any number of events, and any kind of relationship (before, during, after).

**Sychronization Constraints:**
    - ==**Serialization**==: Event A must happen before event B
    - ==**Mutual Exclusion**==: Events A and B must not happen at the same time


Software techniques for enforcing synchronization constraints

within one processor(or one thread) we know the order of execution, but between processors (or threads) it is impossible to tell

Two events are concurrent if we cannot tell by looking at the program which will happen first. that is non-deterministic.

**Shared Variables**
- Concurrent writes
- Concurrent updates e.g. count += 1

An operation that cannot be interrupted is said to be atomic
**mutual exclusion, or mutex**: only one thread accesses a shared variable at a time

**Solutions**
1. Serialization with messages
2. Mutual exclusion with messages

##Chapter 2 Semaphore
invented by Edsger Dijkstra

**Definition**
like an integer
1. When you create the semaphore, ==**you can initialize its value to any integer**==, but after that the only operations you are allowed to perform are increment(increase by one) and decrement (decrease by one). ==**You cannot read the current value of the semaphore.**==
1. When a thread decrements the semaphore, if the result is negative, the thread ==**blocks**== itself and cannot continue until another thread increments the semaphore.
1. When a thread increments the semaphore, if there are other threads waiting, one of the waiting threads gets unblocked.

``` {highlight=[12-13]}
fred = Semaphore (1)

fred . increment ()
fred . decrement ()

fred . signal ()
fred . wait ()
 
fred .V()
fred .P()

fred . increment_and_wake_a_waiting_process_if_any ()
fred . decrement_and_block_if_the_result_is_negative ()
```

##Cahpter 3 Basic Synchronization Patterns

**Signaling**
**Rendezvous**
Thread A has to wait for Thread B and vice versa
Deadlock
```
Thread A:

bArrived.wait()
aArrived.signal()

Thread B:

aArrived.wait()
bArrived.signal()

```
**Mutex**
1 thread can run in the critical section at the same time
Create a semaphore named mutex that is initialized to ==1==.

A value of one means that a thread may proceed and access the shared variable; 
A value of zero means that it has to wait for another thread to release the mutex.

Often the code that needs to be protected is called the ==**critical section**==

```
Thread A:
mutex.wait ()
    # critical section
    count = count + 1
mutex.signal ()

Thread B:
mutex.wait ()
    # critical section
    count = count + 1
mutex.signal ()
```

**Multiplex**
no more than n threads can run in the critical section at the same time
initialize the semaphore to n
```
multiplex . wait ()
    critical section
multiplex . signal ()
```
**Barrier**
The synchronization requirement is that no thread executes critical point until after all threads have executed rendezvous.

When the first n − 1 threads arrive they should block until the n^th^ thread arrives, at which point all the threads may proceed.

**Reusable Barrier**

**Queue**



##Chapter 4 Classical sychronziation problems

###4.1 Producer-consumer problem
Event-driven programs
* Whenever an event occurs, a producer thread creates an event object and adds it to the event buffer
* Concurrently, consumer threads take events out of the buffer and process them.

access to the buffer has to be exclusive  but `waitForEvent` and 'event.process' can run concurrently

```
# Producer-consumer initialization
mutex = Semaphore(1) # for exclusive access to the buffer
items = Semaphore(0) # for blocking the waiting thread when there is no event
# if items is positive, it indicates the number of items in the buffer
# if items is negative, it indicates the number of consumer threads in the queue
local event
```
event is a local variable, which in this context means that each thread has its own version.
```
# Producer Code
event = waitForEvent()
mutex.wait()
    buffer.add(event)
    items.signal()
mutex.signal()
```
```
# Consumer Code
items.wait()
mutex.wait()
    event = buffer.get()
mutex.signal()
event.process()
```

==any time you wait for a semaphore while holding a mutex, there is a danger of deadlock==
## Producer-consumer with a finite buffer
* If a producer arrives when the buffer is full, it blocks until a consumer removes an item.

But we can’t check the current value of a semaphore
Thus add **a second semaphore** to keep track of the number of available spaces in the buffer.

## 4.2 Readers-writers problem