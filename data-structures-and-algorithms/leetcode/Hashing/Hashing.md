# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Hashing](#hashing)
  - [What is the point of a hash function?](#what-is-the-point-of-a-hash-function)
  - [Comparison with arrays](#comparison-with-arrays)
  - [Sets](#sets)
  - [Arrays as keys?](#arrays-as-keys)
  - [Interface guide](#interface-guide)


## Hashing

Before we start this chapter, let's quickly talk about data structures.

In the most basic terms, a data structure is a format for organizing data in an efficient way. In practical terms, we can split data structures into two things: the interface and the implementation.

The **interface** is like a contract that specifies how we can interact with the data structure - what operations we can perform on it, what inputs it expects, and what outputs we can expect. Basically, it's how we use the data structure.

For example, consider a dynamic array. The interface would include operations like appending, insertion, removal, updating, and more. These operations are well-defined and have specific rules that we must follow when we use them. If we want to append an element, we use the built-in method like `.append()` or `.push()` while passing in the element we want to add as an argument. Typically this operation doesn't return anything.

The **implementation** is the code that actually makes the data structure work. This is where the details of how the data is stored and how the operations are performed come into play. For example, the implementation of a dynamic array might involve allocating memory for the list, tracking the size, and rearranging the elements when an operation like remove is called.

For many data structures, the implementation can be quite complex, involving intricate algorithms and data manipulation. However we don't need to worry about those details - we only need to understand the interface and how to use it properly.

In this chapter, we are going to talk about hash maps and sets, which are implemented using [hashing](https://en.wikipedia.org/wiki/Hash_function).

A hash function is a function that takes an input and deterministically converts it to an integer that is less than a fixed size set by the programmer. Inputs are called **keys** and the same input will always be converted to the same integer. Here's an example hash algorithm for a string containing letters of the English alphabet:

- Declare an integer `total`.
- Iterate over the string. For each character, convert it to its position in the alphabet. For example, `a -> 1`, `c -> 3`, `z -> 26`.
- Take that value, and multiply it by the current position in the string (index + 1). Add this to `total`. For example, given the string `"abc"`, the `b` is at position `2` in the alphabet and position `2` in the string, so it would contribute `2 * 2 = 4` towards `total`.
- After going through every character, `total` is the converted value.


This algorithm isn't actually a good hash function but is just an example of how one could convert strings into integers. You may be wondering: don't we need to limit `total` to a fixed size? Correct! Right now, this algorithm is wrong. Let's say the limit we set was x. Then change step `4` to:

- After going through every character, `total % x` is the converted value.
- `%` is the [modulo operation](https://en.wikipedia.org/wiki/Modulo), and makes sure the final converted value will be in the range `[0, x - 1]`.

## What is the point of a hash function?

We know that arrays have $O(1)$ random access. Given an arbitrary index, we can access and update its value in the array in constant time. The main constraint with arrays is that they are a fixed size, and the indices have to be integers. Because hash functions can convert any input into an integer, we can effectively remove the constraint of indices needing to be integers. When a hash function is combined with an array, it creates a **hash map**, also known as a **hash table** or **dictionary**.

With arrays, we **map** indices to values. With hash maps, we map **keys** to values, and a key can be almost anything. Typically, the only constraint on a hash map's key is that it has to be **immutable** (this is language dependent but generally a good rule of thumb). Values can be anything.

A hash map is probably the most important concept in all of algorithm interviewing. It is extremely powerful and allows you to reduce the time complexity of an algorithm by a factor of $O(n)$ for a huge amount of problems. Every major language has a [built-in implementation of a hash map](https://en.wikipedia.org/wiki/Hash_table#Implementations). For example, in Python they're called dictionaries and declaring one is as simple as `dic = {}`. If you could only take one thing from this course, it should be to master the hash map interface for the programming language you use.

To summarize, a hash map is an unordered data structure that stores key-value pairs. A hash map can add and remove elements in $O(1)$, as well as update values associated with a key and check if a key exists, also in $O(1)$. You can iterate over both the keys and values of a hash map, but the iteration won't necessarily follow any order (there are many implementations and this is language dependent for the built-in types).

> An ordered data structure is one where the insertion order is "remembered". An unordered data structure is one where the insertion order is not relevant.

## Comparison with arrays

In terms of time complexity, hash maps blow arrays out of the water. 

The following operations are all $O(1)$ for a hash map:
- Add an element and associate it with a value
- Delete an element if it exists
- Check if an element exists

A hash map also has many of the same useful properties as an array with the same time complexity:

- Find length/number of elements
- Updating values
- Iterate over elements

> Hash maps are also just easier/cleaner to work with. Even if your keys are integers and you could get away with using an array, if you don't know what the max size of your key is, then you don't know how large you should size your array. With hash maps, you don't need to worry about that, since the key will be converted to a new integer within the size limit anyways.

However, from a practical perspective, there are some disadvantages to using hash maps, and it's important to know them as it is common in interviews to talk about tradeoffs.

The biggest disadvantage of hash maps is that for smaller input sizes, they can be slower due to overhead. Because big $O$ ignores constants, the $O(1)$ time complexity can sometimes be deceiving - it's usually something more like $O(10)$ because every key needs to go through the hash function.

Hash tables can also take up more space. Dynamic arrays are actually fixed-size arrays that resize themselves when they go beyond their capacity. Hash tables are also implemented using a fixed size array - remember that the size is a limit set by the programmer. The problem is, resizing a hash table is much more expensive because every existing key needs to be re-hashed, and also a hash table may use an array that is significantly larger than the number of elements stored, resulting in a huge waste of space. Let's say you chose your limit as 10,000 items, but you only end up storing 10. Okay, you could argue that 10,000 is too large, but then what if your next test case ends up needing to store 100,000 elements? The point is, when you don't know how many elements you need to store, arrays are more flexible with resizing and not wasting space.

> Note: remember that time complexity functions only involve the variables you define. When we say that hash map operations are 
$O(1)$, the variable we are concerned with is usually $n$, which is the size of the hash map. However, this may be misleading. For example, hashing a string requires $O(m)$ time, where 
$m$ is the length of the string. The constant time operations are only constant **relative to the size of the map**.

## Sets

A set is another data structure that is very similar to a hash table. It uses the same mechanism for hashing keys into integers. The difference between a set and hash table is that sets do not map their keys to anything. Sets are more convenient to use when you only care about checking if elements exist. You can add, remove, and check if an element exists in a set all in $O(1)$.

An important thing to note about sets is that they don't track frequency. If you have a set and add the same element 100 times, the first operation adds it and the next 99 do nothing.

> A set is basically a hash map if you only consider the keys.

## Arrays as keys?

We said that being immutable is usually a requirement for being a hash map key. Arrays are mutable, so how do we store an ordered collection of elements as a key? Depending on the language you're using, there are several ways to convert an array into a unique immutable key. In Python, tuples are immutable, so it's as easy as doing `tuple(arr)`. Another trick is to convert the array into a string, delimited by some character that is guaranteed to not show up in any element. For example, use a comma to separate integers. `[1, 51, 163]` --> `"1,51,163"`.

> In some languages, there may be data structures that allow you to associate mutable data structures to values. For example, in C++ there is `std::map`. Note that these are not hash maps, but they can be used to solve similar problems.

## Interface guide

Here's a quick runthrough of the interface for a hash map:

```python
# Declaration: a hash map is declared like any other variable. The syntax is {}
hash_map = {}

# If you want to initialize it with some key value pairs, use the following syntax:
hash_map = {1: 2, 5: 3, 7: 2}

# Checking if a key exists: simply use the `in` keyword
1 in hash_map # True
9 in hash_map # False

# Accessing a value given a key: use square brackets, similar to an array.
hash_map[5] # 3

# Adding or updating a key: use square brackets, similar to an array.
# If the key already exists, the value will be updated
hash_map[5] = 6

# If the key doesn't exist yet, the key value pair will be inserted
hash_map[9] = 15

# Deleting a key: use the del keyword. Key must exist or you will get an error.
del hash_map[9]

# Get size
len(hash_map) # 3

# Get keys: use .keys(). You can iterate over this using a for loop.
keys = hash_map.keys()
for key in keys:
    print(key)

# Get values: use .values(). You can iterate over this using a for loop.
values = hash_map.values()
for val in values:
    print(val)
```