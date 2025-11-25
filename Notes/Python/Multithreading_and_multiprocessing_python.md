# Multithreading & Multiprocessing with Python

## 'What is a Program?':
- A program is a sequence of instructions written in a programming language.
- Stored on disk and not running until executed.
- Examples: Chrome, MS Word, Excel.

---

## 'What is a Process?':
-A running instance of a program.
-Each process has its own separate memory space.
-Identified using PID (Process ID).

---

## 'What is a Thread?':-
-Smallest unit of execution inside a process.
-Multiple threads run within the same process.
-Threads share:
  -Code segment
  -Data segment
  -Heap
-Each thread has its own Stack + Registers.

----

## 'Execution Control Functions ' :
1.start()
- start() is used to begin the execution of a thread or process.
- After calling start(), the thread/process runs independently in the background.

2.join()
- Blocks the main program flow until the target thread or process has completed its execution. This ensures synchronization

----
## 'What is Multithreading?':
-Running multiple threads inside one process.
-Best for I/O Bound tasks (waiting time tasks)
-Example: File download, Web scraping, Database operations.

1.Import Module

```py
import threading
import time
```
2.Multithreaded Execution
```py
def print_numbers():
    for i in range(5):
        print(i)
        time.sleep(2)

def print_letters():
    for c in "ABCD":
        print(c)
        time.sleep(2)

t1 = threading.Thread(target=print_numbers)
t2 = threading.Thread(target=print_letters)
t1.start()
t2.start()
t1.join()
t2.join()

```
---
## 'What is Multiprocessing? ' :
-Running multiple processes in parallel.
-Best for CPU Bound tasks (heavy computation).
-Uses multiple CPU cores.
 

1.Import Module
```py
import multiprocessing
import time
```
2.multiprocessing Execution
```py
def square():
    for i in range(5):
        print(i*i)
        time.sleep(1)

def cube():
    for i in range(5):
        print(i*i*i)
        time.sleep(1.5)

if __name__ == "__main__":
    p1 = multiprocessing.Process(target=square)
    p2 = multiprocessing.Process(target=cube)
    p1.start()
    p2.start()
    p1.join()
    p2.join()

```

---
## 'ThreadPoolExecutor (Multithreading)':
- Used for multithreading.
- Runs tasks using multiple threads inside one process.
- It manages a pool of multiple threads automatically, so you don’t need to create threads manually one by one.
- Best for I/O bound tasks (web scraping, file downloading, database queries).

# How it works
- You give a function and a list of inputs.
- It assigns multiple threads to run the function concurrently.
- Improves speed because while one thread waits (I/O delay), other threads continue execution.

```py
from concurrent.futures import ThreadPoolExecutor
import time

def print_number(n):
    time.sleep(1)
    return f"Number: {n}"

numbers = [1,2,3,4,5]
with ThreadPoolExecutor(max_workers=3) as executor:
    results = executor.map(print_number, numbers)

for r in results:
    print(r)

```

---
## 'ProcessPoolExecutor (Simplified Multiprocessing)':
- Used for multiprocessing.
- Runs tasks using multiple processes across CPU cores.
- It manages a pool of processes automatically, so you don’t need to create    processes manually.
- Best for CPU bound tasks (heavy calculations, image/video processing).

# 'How it works':
- You give a function and a list of inputs.
- It assigns tasks to multiple CPU cores, running each in a separate process.
- Improves speed because multiple CPU cores work in parallel.

```py
from concurrent.futures import ProcessPoolExecutor
import time

def square(n):
    time.sleep(1)
    return n*n

if __name__ == "__main__":
    numbers = [1,2,3,4,5]
    with ProcessPoolExecutor(max_workers=3) as executor:
        results = executor.map(square, numbers)

for r in results:
    print(r)

```

---
## 'Real-World Use Cases':
|Technique      |Best Used For                                                  |
|---------------|---------------------------------------------------------------|
|Multithreading	|I/O bound tasks (web scraping, file/network operations)        |
|Multiprocessing |CPU bound tasks (mathematics, ML training, video/image  processing)|

---
## 'Key Takeaways':
-Program → set of instructions.
-Process → executing program with its own memory.
-Thread → execution unit inside a process.
-Multithreading → concurrency for I/O tasks.
-Multiprocessing → parallelism for CPU tasks.
-ThreadPoolExecutor → easy multithreading.
-ProcessPoolExecutor → easy multiprocessing.