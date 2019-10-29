Synchronization constraints:
* Serialization: Event A must happern before Event B
* Mutual Exclusive: Event A and Event B must not happen at the same time

Two events are concurrent if we cannot tell by looking at the program which will happen first
Concurrent programs are often non-deterministic

Thread Interaction:
* Concurrent Writes
* Concurrent Updates
    * reads the value of a variable
    * computes a new value  
    * writes the new value

An operation that cannot be interrupted is said to be atomic

Mutual exclusion with messages

---

Semaphores
* Positive Value
it represents the number of threads that can decrement without blocking.
* Negative Value
it represents the number of threads that have blocked and are waiting.
* Zero
it means there are no threads waiting.

You cannot read the current value of the semaphore.

``` python
fred = Semaphore(1) # constructor, initial value is 1
# operations
fred.increment_and_wake_a_waiting_process_if_any() # fred.signal()
fred.decrement_and_block_if_the_result_is_negative() # fred.wait()


```