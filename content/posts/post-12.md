---
title: "Engineering behind Mutable and Immutable in Python"
date: 2024-12-27T15:46:13+05:45
draft: false
description: Explore the core engineering concepts behind mutable and immutable data types in Python with simple explanations and practical examples.
tags: ["Python", "Programming", "Mutable", "Immutable", "Memory Management"]
---


If you’ve been programming in Python, you’ve probably come across the terms *mutable* and *immutable*. These words might sound casual, but have you ever wondered how mutable is actually mutable? and immutable immutable? Its quite simple once you get the hang of it. Let's break it down and look at the "how" and "why" behind these concepts.

---

### What Do Mutable and Immutable Mean?

- **Mutable** means *changeable*. Data types like lists, sets, and dictionaries can be modified after they are created.
- **Immutable** means *unchangeable*. Data types like strings, integers, and tuples cannot be altered once they are created.

Now, here’s where it gets interesting: even if a data type is immutable, it doesn’t mean you can’t assign new values to a variable. Let’s go a bit further.

---

### Example 1: Strings Are Immutable

```python
>>> username = "karan"
>>> username
'karan'
>>> username = "notkaran"
>>> username
'notkaran'
```

Strings are immutable, so when you assign a new value to the variable `username`, Python doesn’t overwrite the old value. Instead:

1. A new memory block is created for the new value `"notkaran"`.
2. The variable `username` is updated to reference this new block.
3. The old value `"karan"` is left behind and will be deleted later by Python’s garbage collector, but only if no other variable is using it.

#### Memory Allocation Diagrams

![karan](/images/userkaran.png)
*when username = "karan"*

![notkaran](/images/usernotkaran.png)
*after re-assigning the value when username = "notkaran"*

Here, the value `"karan"` is stored at a different memory location, which will be removed by the garbage collector in Python since no variable is referencing it.

---

### Example 2: Integers and Memory Allocation

```python
>>> x = 10
>>> y = x
>>> x = 20
>>> x
20
>>> y
10
```

In this case:

- Initially, `x` and `y` both reference the same value `10` in memory.
- When you assign `20` to `x`, Python creates a new memory block for `20` and updates `x` to reference this new block.
- The value `10` is still in memory because `y` is referencing it.

#### Memory Allocation Diagram

![xandy](/images/xandy.png)
*In this case, the value `10` won’t be deleted as it is being referenced by `y`.*

---

### Why Does This Matter?

The distinction between mutable and immutable types is crucial for **Performance** as Immutable objects are often faster because they don't need mechanisms to handle changes. And **Data Safety** is another reason as Immutable types prevent accidental modifications, making them ideal for constants and keys in dictionaries.

---

### The Core Engineering Behind Mutability

At the heart of Python’s design lies its memory management system and here is how it works:

- **Mutable types** like lists and dictionaries store data in a memory buffer that can be altered directly.
- **Immutable types** don’t allow changes to the data in memory. Instead, new memory is allocated for any modifications.

This ability to allocate new memory or update existing memory is what makes mutability possible (or impossible) at its core.

