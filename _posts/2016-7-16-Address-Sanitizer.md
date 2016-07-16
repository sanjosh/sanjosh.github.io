
Summary of Address Sanitizer paper

## Address Sanitizer has two components : 
1. LLVM-time instrumentation
2. Runtime

### Type of memory objects
1. stack
2. heap
3. global

### Type of errors to detect
1. use-before-alloc (i.e. out of bounds)
2. use-after-free (access after free)
3. read-before-write (i.e. uninitialized read)


### Use of Shadow memory
- taks about 1/8th of actual memory
- one byte for each 8 bytes of alloc
- byte indicates if corresponding memory is allocated/initialized/free

### Instrumentation added to code
- Inserts code during an LLVM pass
- insert code to check shadow state for each memory access
- create poison zones around stack and global objects

### Runtime component
- malloc() create redzones of 32 bytes around every object
- this redzone stores alloc_size, threadId, call stack
- free() poisons the region and uses a queue to ensure it doesnt get allocated anytime soon
- each memory access checks if corresponding shadow byte is zero

###Thread-safe by design
- Shadow mem modified only inside malloc/free, stack frame create/destroy, module init
- All other thread-related accesses to shadow memory are reads


[ Address Sanitizer paper] (http://research.google.com/pubs/pub37752.html)
