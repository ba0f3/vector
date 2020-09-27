# Introduction
A simple reallocating vector library for nim.

The vector's buffer extends when you add an item using ``push`` or ``extend`` by a power of 2 when it runs out of memory.

For example:

```nim
var vec = initVector[int]()  # vec's buffer size is 4 (int.sizeof())

vec.extend(@[1, 2, 3, 4, 5])  # vec's buffer size is 32
# 32 is the lowest power of 2 that is bigger than 20 (5 * int.sizeof())
```

# Notes
The buffer never resizes down (shrinks).

If you really want to shrink your vector, you can allocate a new one using the old one:

```nim
var vec = initVector[uint8](1000)  # vec's buffer size is 1024
vec.clear()  # still 1024
var newVec = initVector(vec)  # newVec's buffer size is now float.sizeof()
```
