https://realpython.com/intro-to-python-threading/

---

A thread is a separate flow of execution. 
GIL limits one Python thread to run at a time. 
* Tasks that spend much of their time waiting for external events are generally good candidates for threading. 
* Problems that require heavy CPU computation and spend little time waiting for external events might not run faster at all. 

---

To start a thread
``` python
import threading
x = threading.Thread(target=thread_function, args=(1,))
x.start()
```

Daemon threads
a daemon is a process that runs in the background.
In python, a daemon thread will shut down immediately when the program exits.
``` python
x = threading.Thread(target=thread_function, args=(1,), daemon=True)
```

To tell one thread to wait for another thread to finish
```python
# x.join()
threads = list()
for index in range(3):
    x = threading.Thread(target=thread_function, args=(index,))
    threads.append(x)
    x.start()
for index, thread in enumerate(threads):
    thread.join()
```

---

**ThreadPoolExecutor** works  as a context manager. 
The end of the with block automatically do a .join() on each of the threads in the pool.
```python
import concurrent.futures
with concurrent.futures.ThreadPoolExecutor(max_workers=3) as executor:
        executor.map(thread_function, range(3))

# submit(function, *args, **kwargs)
with concurrent.futures.ThreadPoolExecutor(max_workers=2) as executor:
    for index in range(2):
        executor.submit(thread_function, index)
```



Note: Using a ThreadPoolExecutor can cause some confusing errors.
For example, if you call a function that takes no parameters, but you pass it parameters in .map(), the thread will throw an exception.
Unfortunately, ThreadPoolExecutor will hide that exception, and (in the case above) the program terminates with no output. This can be quite confusing to debug at first.

---

## Race Conditions
occur when two or more threads access a shared piece of data or resource.
Even an operation like x += 1 takes the processor many steps. 
The operating system can swap which thread is running at any time.

## Threading.Lock() 
The basic functions to do this are .acquire() and .release().
with threading.Lock()
```python
class FakeDatabase:
    def __init__(self):
        self.value = 0
        self._lock = threading.Lock()

    def locked_update(self, name):
        with self._lock:
            local_copy = self.value
            local_copy += 1
            time.sleep(0.1)
            self.value = local_copy
```
RLock allows a thread to .acquire() an RLock multiple times before it calls .release(). That thread is still required to call .release() the same number of times it called .acquire()

---

## Producer-Consumer Threading
threading or process synchronization issues
