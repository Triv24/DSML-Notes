# Memory Management with Python :

- Memory Management in python involves a combination of automatic garbage collection, reference counting, and various internal optimisations to efficiently manage memory allocation and deallocation.
- Understanding these mechanisms can help developers write more efficient and robust applications.

    1. Key concepts in Python Memory mgmt
    2. Memory allocation and deallocation
    3. Reference counting
    4. Garbage collection
    5. The `gc` module
    6. Memory management Best practices

## Reference counting :

- Reference counting is the primary method Python uses to manage memory.
- Each object in python maintains a count of references pointing to it.
- When the reference count drops to zero, the memory occupied by the object is deallocated.

```py
import sys

a = []

print(sys.getrefcount(a))

```

- Output : `2`

- This is happening because the list has 2 references : 
    1. the variable `a`
    2. the function `getrefcount()`

- if we add one more reference to the list : `b = a`
    - the output will be 3
    - then if we `del b`, the output will again give answer 2

## Garbage Collection in Python :

- Python includes a cyclic garbage collector to handle reference cycles.
- Reference cycles occur when objects reference each other, preventing their reference counts from reaching zero.

```py
import gc

# Enable garbage collection
gc.enable()

# Disable Garbage collection :
gc.disable()

# Manually trigger garbage collection :
gc.collect() # return the number of unreachable variables

# get garbage collection stats :
gc.get_stats() # returns a list of dictionaries 

output of get_stats() :
[
    {
        'collections' : 182,
        'collected' : 1611,
        'uncollectable' : 0
    },
    {
        'collections' : 182,
        'collected' : 1611,
        'uncollectable' : 0
    }
]


# Get unreachable objects :
print(gc.garbage)
```

## Memory Management Best Practices :

1. Use local variables :
    - Local variables have a shorter life span and arre freed sooner than global variables.

2. Avoid Circular references :
    - Circular references can lead to memory leas if not properly managed.

3. Use Generators :
    - Generators produce items one at a time and only keep one item in memory at a time, making them memory efficient.

4. Explicitly delete objects :
    - Use `del` statement to delete variables and objects explicitly.

5. Profile Memory Usage : 
    - Use **memory profiling tools** like :
        - `tracemalloc`
        - `memory_profiler`
    - to identify memory leaks and optimise memory usage.

### Handling circular reference by manually triggering garbage collection

```py
import gc

class MyObj :
    def __init__(self, name) :
        self.name = name
        print(self.name)

    def __del__(self) :
        print(self.name + " deleted")

## circular reference :
obj1 = MyObject("Obj1")
onj2 = MyObject("obj2")

obj1.ref = obj2
obj2.ref = obj1

# trying to delete objects :
del obj1
del obj2
# -- But they will not get deleted because of circular reference
# -- Hence we will have to trigger garbage collection

## Manually trigger garbage collection
gc.collect()
```

### Using Generator for memory efficiency :

```py
def generate_numbers(n) :
    for i in range(n):
        yield i

for num in generate_numbers(10000000) :
    print(num)
    if num > 10 :
        break
```

### Profiling memory usage :
- Tracing the memory usage using the module named `tracemalloc`

```py
import tracemalloc

def create_list() :
    return [i for i in range(10000)]

def main() :
    tracemalloc.start()

    create_list()

    snapshot = tracemalloc.take_snapshot()
    top_stats = snapshot.statistics('lineno')

    print("Top 10")
    for stat in top_stats[:10]:
        print(stat)

```