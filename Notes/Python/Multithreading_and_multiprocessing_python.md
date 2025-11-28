# Multithreading & Multiprocessing with Python

## What is a Program?
- A program is a sequence of instructions written in a programming language.
- Stored on disk and not running until executed.
- Examples: Chrome, MS Word, Excel.

---

## What is a Process?
- A running instance of a program.
- Each process has its own separate memory space.
- Identified using PID (Process ID).

---

## What is a Thread?
- Unit of execution within a process.
- single threaded process - one single thread running at a time.
- multi-threaded process
- Multiple threads run within the same process.
- Threads share:
  - Code segment
  - Data segment
  - Heap
- Each thread has its own Stack + Registers.

----

## Execution Control Functions  
1.start()
- start() is used to begin the execution of a thread or process.
- After calling start(), the thread/process runs independently in the background.

2.join()
- Blocks the main program flow until the target thread or process has completed its execution. This ensures synchronization

----
## What is Multithreading?
- Running multiple threads inside one process.
- Best for I/O Bound tasks (waiting time tasks)
- Example: File download, Web scraping, Database operations.

### When to use multi-threading ?
1. I/O Bound your applicationtasks : Tasks that spend more time waiting for I/O operations
2. Concurrent execution : When you want to improve the throughput of 

### 1.Import Module

```py
import threading
import time
```

### 2.Multithreaded Execution

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


# Starting the thread
t1.start()
t2.start()

# Wait for the thread to be completed and then simply join to the main thread
t1.join()
t2.join()

```
---

## What is Multiprocessing?  
- Running multiple processes in parallel.
- Best for **CPU Bound tasks** (heavy computation).
- Uses **multiple CPU cores**.
 

### 1.Import Module
```py
import multiprocessing
import time
```
### 2.multiprocessing Execution
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

    # Start the processes
    p1.start()
    p2.start()

    # wait for the processes to complete
    p1.join()
    p2.join()

```

---
## `ThreadPoolExecutor` (Multithreading) :

- Used for multithreading.
- Runs tasks using multiple threads inside one process.
- It manages a pool of multiple threads automatically, so you don’t need to create threads manually one by one.
- Best for I/O bound tasks (web scraping, file downloading, database queries).

### How it works
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
## `ProcessPoolExecutor` (Simplified Multiprocessing)
- Used for multiprocessing.
- Runs tasks using multiple processes across CPU cores.
- It manages a pool of processes automatically, so you don’t need to create    processes manually.
- Best for CPU bound tasks (heavy calculations, image/video processing).

### How it works
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
## Real-World Use Cases
|Technique       |Best Used For                                                  |
|--------------- |---------------------------------------------------------------|
|Multithreading	 |I/O bound tasks (web scraping, file/network operations)        |
|Multiprocessing |CPU bound tasks (mathematics, ML training, video/image  processing)|

---
## Web Scraping :
- Web scraping often involves making numerous network requests to fetch web pages.
- These tasks are **I/O bound** because they wait for server responses. 
- Multithreading improves performance by allowing multiple pages to be fetched concurrently.

---

### Selecting URLs for Scraping

Store the target URLs in a list:

```py
urls = [
    "https://example.com/page1",
    "https://example.com/page2",
    "https://example.com/page3"
]
```
### Importing Required Libraries
-We need:
    - threading for creating threads
    - requests for HTTP requests
    - `bs4` (BeautifulSoup) for parsing HTML

```py
import threading
import requests
from bs4 import BeautifulSoup
```

### Defining the Web Scraping Function
- A simple function to fetch a URL and print the number of characters in the page text:

```py
def fetch_contents(url):
    try:
        response = requests.get(url, timeout=10)
        response.raise_for_status()
        soup = BeautifulSoup(response.content, "html.parser")
        print(f"Fetched {len(soup.get_text())} characters from {url}")
    except requests.RequestException as e:
        print(f"Failed to fetch {url}: {e}")

threads = []

# creating and starting threads :
for url in urls :
    thread = threading.Thread(target=fetch_contents, args = (url))
    threads.append(thread)
    thread.start()

# Waiting for thread to be completed :
for thread in threads :
    thread.join()
      
```

##### Notes:
- timeout prevents hanging.
- raise_for_status() raises for HTTP errors.
- soup.get_text() extracts visible text.


## Real-World implementation of Multiprocessing :
- Real world Example : Multiprocessing for **CPU Bound Tasks**
- **Scenario** : Factorial calculation

- Factorial calculations, especially for large numbers, involve significant computational work. 
- Multiprocessing can be used to distribute the workload across multiple CPU cores, improving performance.

```py
import multiprocessing
import math
import sys
import time

# Increase the maximum number of digits for integer conversion
sys.set_int_max_str_digits(100000)

## Function to compute factorial of a given number
def compute_factorial (number) :
    print("Factorial : ")
    result = math.factorial(number)
    return result

if __name__ == "__main__" :
    numbers = [5000, 6000, 70000]

    start_time = time.time()

    ## Create a pool of worker processes
    with multiprocessing.Pool() as pool :
        results = pool.map(compute_factorial, numbers)

    end_time = time.time()

    print(end_time - start_time)

    print(results)
```

---
## Key Takeaways:
- Program → set of instructions.
- Process → executing program with its own memory.
- Thread → execution unit inside a process.
- Multithreading → concurrency for I/O tasks.
- Multiprocessing → parallelism for CPU tasks.
- ThreadPoolExecutor → easy multithreading.
- ProcessPoolExecutor → easy multiprocessing.