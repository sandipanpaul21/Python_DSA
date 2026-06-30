# Topic: Loops in Python

> Covers: `range()`, `len()`, `for` loop, `while` loop, `break`, `continue`, `pass`, Nested Loops

---

## 1. Introduction

* **What is it?** A loop is a control structure that repeats a block of code multiple times.
* **Definition:** A loop executes a set of statements again and again, either a fixed number of times or until a condition becomes False.
* **Why do we need it?**
  * Avoids writing the same line of code repeatedly.
  * Lets a program handle data of any size (10 items or 10 million) with the same few lines.
  * Follows the DRY principle — Don't Repeat Yourself.
* **Where is it used?**
  * Processing every item in a list, file, or database table.
  * Validating user input until it is correct.
  * Game loops (keep running until the player quits).
  * Repeating a calculation until a desired accuracy is reached.

---

## 2. Real-Life Analogy

* **Loop (general):** A washing machine's wash cycle — it repeats the same rinse-spin action automatically until the clothes are clean, instead of you rinsing each piece by hand.
* **`for` loop:** A teacher calling out roll numbers 1 to 40 — a fixed, known list, one item at a time, in order.
* **`while` loop:** Boiling water on a stove — you keep checking "has it boiled yet?" and stop only when the condition is met; you don't know the exact count in advance.
* **`break`:** Searching for car keys drawer by drawer — the moment you find them, you stop checking the remaining drawers.
* **`continue`:** Sorting a basket of apples — when you spot a rotten one, you skip it and move straight to the next apple, without stopping the sorting.
* **`pass`:** A parking spot with a "Reserved" sign — nothing happens there yet, but it is acknowledged and saved for later.
* **Nested loop:** A wall clock — the minute hand (inner loop) completes a full round for every single tick of the hour hand (outer loop).

---

## 3. Explanation

* A loop has two parts: a **condition** that controls how long it runs, and a **body** that runs repeatedly.
* Python has two loop keywords:
  * `for` — used when you already know the collection you are looping over (a string, list, range, etc.). Called a **definite loop**.
  * `while` — used when the number of repetitions depends on a condition that may change at runtime. Called an **indefinite loop**.
* `range()` generates a sequence of numbers on demand, without storing them all in memory at once.
* `len()` returns the count of items in a string, list, tuple, or dictionary.
* `break`, `continue`, and `pass` change the normal top-to-bottom flow inside a loop body.
* A loop inside another loop is a **nested loop** — useful for anything with two dimensions, like rows and columns.

---

## 4. Syntax

**`range()`**
```python
range(stop)                # 0, 1, 2, ... stop-1
range(start, stop)         # start, start+1, ... stop-1
range(start, stop, step)   # jumps by 'step' each time
```
* `start` — first number (default 0).
* `stop` — loop stops before this number; it is never included.
* `step` — amount added each time (default 1, can be negative to count down).

**`len()`**
```python
len(object)
```
* `object` — any string, list, tuple, dict, or set. Returns an integer count.

**`for` loop**
```python
for item in iterable:
    # body
```
* `item` — a new variable that holds the current value on each pass.
* `iterable` — anything that can be looped over: string, list, range, dict, etc.

**`while` loop**
```python
while condition:
    # body
```
* `condition` — any expression that evaluates to True or False. Loop runs while it is True.

**`break` / `continue` / `pass`**
```python
break       # exits the loop immediately
continue    # skips to the next iteration
pass        # does nothing, just a placeholder
```

**Nested loop**
```python
for outer_item in outer_iterable:
    for inner_item in inner_iterable:
        # innermost body
```

---

## 5. Examples

### Basic Example
```python
for num in range(1, 6):
    print(num)
```
* `range(1, 6)` creates the sequence 1, 2, 3, 4, 5.
* `for num in ...` takes one value at a time and stores it in `num`.
* `print(num)` runs once per value.
* Output: `1 2 3 4 5` printed on separate lines.

### Intermediate Example
```python
attempts = 0
max_attempts = 3
correct_pin = "4521"

while attempts < max_attempts:
    entered_pin = input("Enter your PIN: ")
    if entered_pin == correct_pin:
        print("Access Granted")
        break
    attempts += 1
    print(f"Wrong PIN. Attempts left: {max_attempts - attempts}")
else:
    print("Card Blocked")
```
* `attempts` and `max_attempts` set up the condition for the `while` loop.
* The loop keeps asking for a PIN as long as `attempts < max_attempts`.
* If the PIN matches, it prints success and `break`s out immediately.
* If not, `attempts` increases by 1 and the remaining tries are shown.
* The `else` block on a `while` loop runs only if the loop ends naturally (no `break` happened) — here, all 3 attempts were wrong.

### Real-World Example
```python
contacts = {"Mom": "9876543210", "Boss": "9123456780", "Friend": "9988776655"}
search_name = "Boss"

for name, number in contacts.items():
    if name == search_name:
        print(f"Found {name}: {number}")
        break
else:
    print("Contact not found.")
```
* `contacts.items()` gives each key-value pair (name, number) one at a time.
* The `for` loop checks every contact until it finds a match.
* `break` stops the search the moment the right contact is found — like scrolling through your phone contacts and stopping once you see the right name.
* The `for...else` block runs only if the loop finishes without finding a match.

---

## 6. Internal Working

* **How `for` actually works internally:**
  * Python calls `iter(iterable)` to get an **iterator object**.
  * It then repeatedly calls `next()` on that iterator to get the next value.
  * When there are no more values, the iterator raises a `StopIteration` exception, and Python silently stops the loop.
  * This is called the **iterator protocol**, and it's why strings, lists, dicts, and `range` objects can all be used in a `for` loop — they all know how to produce an iterator.
* **`range()` internals:**
  * A `range` object does not store every number in memory.
  * It only stores `start`, `stop`, and `step`, and calculates each value the moment it is asked for.
  * This is why `range(1, 10000000)` takes almost no memory, unlike a list of the same size.
* **How `while` actually works internally:**
  * There is no iterator protocol involved.
  * Python simply evaluates the condition expression every single time before running the body.
  * At the bytecode level, this is essentially: compare the condition, jump past the loop if False, otherwise run the body and jump back to the comparison.
* **`break`/`continue` internally:** these compile to direct jump instructions in Python's bytecode — `break` jumps to the instruction right after the loop, `continue` jumps back to the loop's condition check.

---

## 7. Time and Space Complexity

* **Single loop** (`for` or `while`) running `n` times:
  * Time Complexity: O(n) — work grows directly with the number of iterations.
  * Space Complexity: O(1) — if you're just using a counter or doing simple work each time, no extra memory grows with `n`.
* **Nested loop** (loop inside a loop), each running roughly `n` times:
  * Time Complexity: O(n²) — for every outer step, the inner loop runs fully again.
  * Space Complexity: O(1) if you're not storing results, or O(n) if you're appending results into a new list.
* **`range()`:**
  * Space Complexity: O(1) regardless of size, because it generates numbers lazily instead of storing them.
* **Why:** complexity is about how the *amount of work* (or memory) scales as input size `n` grows — a single pass through `n` items is linear, two passes nested inside each other is quadratic.

---

## 8. Common Mistakes

* **Off-by-one error** — expecting `range(1, 5)` to include 5. Fix: remember `stop` is excluded; use `range(1, 6)`.
* **Infinite loop** — forgetting to update the variable that controls a `while` condition. Fix: make sure something inside the loop body changes the condition.
* **Using `=` instead of `==`** — `while x = 5:` is invalid; assignment and comparison are different operators.
* **Indentation errors** — inconsistent spacing inside the loop body. Fix: use 4 spaces consistently.
* **Modifying a list while looping over it with `for`** — removing or adding items mid-loop causes skipped elements. Fix: loop over a copy, `for item in my_list[:]:`, or use `while` instead.
* **Missing colon** — forgetting `:` at the end of the `for`/`while` line.
* **Assuming `break` exits all nested loops** — it only exits the innermost loop. Fix: use a flag variable, or move the inner loop into a function and `return` from it.

---

## 9. Best Practices

* Prefer `for item in collection` over `for i in range(len(collection)): item = collection[i]` — it is more readable (Pythonic).
* Use `enumerate(collection)` when you need both index and value, instead of manually tracking an index.
* Use meaningful loop variable names for clarity (`for student in students`) rather than single letters, except for very short, obvious loops (`for i in range(10)` is fine).
* Avoid deeply nested loops (3+ levels) — extract the inner logic into a separate function to keep code readable.
* Never modify a list you are iterating over with `for`; iterate over a copy or rebuild a new list instead.
* Prefer a list comprehension over a `for` loop when you're simply building a new list from an existing one — it's shorter and considered more Pythonic:
  ```python
  squares = [x**2 for x in range(1, 6)]
  ```
* Keep the loop body short; if it grows large, move the logic into a function called from inside the loop.
* Use `while` only when the stopping condition genuinely depends on something that changes at runtime; otherwise prefer `for`.

---

## 10. Interview Questions

**Beginner**
1. What is the difference between `for` and `while` loops?
   Answer: `for` is used when the number of iterations or the collection is already known (definite loop); `while` runs based on a condition that is checked every time, and the number of iterations may not be known in advance (indefinite loop).
2. What does `range(1, 5)` produce?
   Answer: 1, 2, 3, 4 — the stop value 5 is excluded.
3. What is the difference between `break` and `continue`?
   Answer: `break` exits the loop completely; `continue` skips only the current iteration and moves to the next one.

**Intermediate**
1. Can a `while` loop run zero times? Explain.
   Answer: Yes — if the condition is False the very first time it is checked, the body never runs.
2. Why shouldn't you modify a list while iterating over it with a `for` loop?
   Answer: Because the loop tracks position by index internally; removing or adding items shifts the remaining elements, causing some to be skipped or processed twice.
3. What is the purpose of the `else` clause on a `for` or `while` loop?
   Answer: It runs only if the loop completes all its iterations without hitting a `break` — useful for "search and report not found" patterns.

**Advanced**
1. Explain the iterator protocol and how it relates to the `for` loop.
   Answer: `for` calls `iter()` on the object to get an iterator, then calls `next()` repeatedly until `StopIteration` is raised; any object implementing `__iter__` and `__next__` can be used in a `for` loop.
2. Why is `range()` considered memory-efficient compared to a list of the same numbers?
   Answer: `range()` stores only `start`, `stop`, and `step`, and computes each value on demand instead of storing every number in memory.
3. What is the time complexity of two nested loops, each iterating `n` times, and when would this become a real performance issue?
   Answer: O(n²); this becomes a problem as `n` grows large, since the work grows quadratically — for example, comparing every pair of elements in a large list.

---

## 11. Practice

**Easy**
1. Print all even numbers from 1 to 50 using a `for` loop and `range()`.
2. Use a `while` loop to print numbers from 10 down to 1.
3. Loop through the string `"PYTHON"` and print each character on a new line.

**Medium**
1. Write a program that asks the user for numbers one at a time (using a `while` loop) and stops when they type `"stop"`, then prints the sum of all numbers entered.
2. Given a list of numbers, use `break` to find and print the first number greater than 50, or print "Not found" if none exists.
3. Print a multiplication table (1 to 10) for a number entered by the user, using a nested loop only if needed.

**Hard**
1. Write a program using nested loops to print a number pyramid pattern (for example, 5 rows, where row `i` contains numbers from 1 to `i`).
2. Given a list of integers, use `continue` to skip negative numbers and print only the running sum of positive numbers.
3. Simulate a simplified ATM: allow a maximum of 3 PIN attempts using `while`, lock the account using a flag if all attempts fail, and use `break` once the correct PIN is entered.

---

## 12. Revision

* A loop repeats a block of code; `for` is for known/fixed collections, `while` is for condition-based repetition.
* `range(start, stop, step)` always excludes `stop` — this is the most common beginner trap.
* `len()` returns the number of items in any collection.
* `break` exits the loop entirely; `continue` skips to the next iteration; `pass` does nothing and is just a placeholder.
* `break` inside a nested loop only exits the innermost loop.
* `for` internally uses the iterator protocol (`iter()` + `next()` + `StopIteration`); `while` is just a repeated condition check, with no iterator involved.
* `range()` is memory-efficient because it generates numbers lazily instead of storing them all.
* A single loop is O(n) time; nested loops are O(n²) time.
* Common bugs: off-by-one errors, infinite loops, modifying a list while iterating over it.
* Prefer Pythonic patterns: `enumerate()` over manual indexing, list comprehensions for simple list-building, descriptive loop variable names.

---

Let me know if you have any doubts on this Loops topic, or if you'd like to move on to the next topic (for example, Lists, Tuples and Dictionaries, or Functions).
