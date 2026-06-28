# Python Conditional Statements - Complete Notes

> Lesson 1 of our Python series: Basics to Advanced
> Reference book: *Python Crash Course* (Chapter 5 - if Statements)

---

## Table of Contents

1. Introduction to Conditional Statements
2. if Statement
3. else Statement
4. elif Statement
5. Nested Conditional Statements
6. Practical Examples
7. Common Errors and Best Practices

---

## 1. Introduction to Conditional Statements

**The basic idea:**
- In daily life, decisions depend on conditions:
  - If it is raining, take an umbrella; otherwise, leave it at home.
  - If the light is red, stop; if it is green, go.
  - If you have enough money, buy the item; otherwise, wait.
- A **conditional statement** in Python checks whether something is `True` or `False`, and runs a different block of code depending on the answer.

**Why programs need this:**
- Without conditions, a program runs every line top to bottom, the same way, every time.
- Real software must react differently depending on user input, data values, or the current situation.
- Examples: login systems, billing calculators, games, search engines - all rely on decisions.

**Boolean values:**
- Every condition in Python evaluates to one of two values:
  - `True`
  - `False`
- These are called **Boolean values**, and they are the foundation of every if statement.

**Comparison operators** (compare two values, always return `True`/`False`):
- `==` - equal to → `5 == 5` gives `True`
- `!=` - not equal to → `5 != 3` gives `True`
- `>` - greater than → `7 > 3` gives `True`
- `<` - less than → `2 < 5` gives `True`
- `>=` - greater than or equal to → `5 >= 5` gives `True`
- `<=` - less than or equal to → `4 <= 3` gives `False`

> **Interview tip:** A single `=` is an *assignment* ("set this value"). A double `==` is a *question* ("are these equal?"). Confusing the two is one of the most common beginner bugs.

**Logical operators** (combine more than one condition):
- `and` - overall result is `True` only if **both** conditions are `True`
  - Example: `age >= 18 and has_id`
- `or` - overall result is `True` if **at least one** condition is `True`
  - Example: `is_weekend or is_holiday`
- `not` - reverses a value
  - Example: `not is_raining` turns `False` into `True`

**Membership operators:**
- `in` - checks whether a value exists inside a list, string, or other collection
- `not in` - checks that a value does **not** exist inside a collection

```python
toppings = ['mushrooms', 'extra cheese']
print('mushrooms' in toppings)      # True
print('pepperoni' not in toppings)  # True
```

**How Python evaluates a condition, step by step:**
1. Python reads the condition (for example, `age >= 18`).
2. It evaluates the condition down to `True` or `False`.
3. If the result is `True`, it runs the indented block right below the condition.
4. If the result is `False`, it skips that block entirely.
5. The program then continues with whatever code comes next.

---

## 2. if Statement

**Concept:**
- The `if` statement is the simplest decision tool: "if this is true, do this - otherwise, do nothing."
- Real-life comparison: a security guard at a building entrance.
  1. If your ID card is valid, you are let in.
  2. If not, nothing happens - you simply aren't let in, and the guard moves on.

**Syntax:**
```python
if condition:
    # this indented block runs ONLY if condition is True
```

> **Important:** Python uses indentation (normally 4 spaces) instead of curly braces `{}` to mark which lines belong inside the if block. This is required by the language, not just a style choice.

**Example - voting eligibility:**
```python
age = 19

if age >= 18:
    print("You are old enough to vote!")
    print("Have you registered to vote yet?")
```
- `age` is `19`, so `age >= 18` is `True`.
- Both `print` lines run, because both are indented inside the if block.
- If `age` were `15` instead, the program would print nothing at all - the entire indented block would be skipped.

**Example - weather reminder:**
```python
weather = "rainy"

if weather == "rainy":
    print("Take an umbrella before you leave.")
```

**Real-time applications:**
- An ATM checks `if balance >= withdrawal_amount` before allowing cash to be withdrawn.
- An e-commerce site checks `if quantity_in_stock > 0` before showing an "Add to Cart" button.

---

## 3. else Statement

**Concept:**
- `if` alone only says what to do when something is true - it says nothing about what happens otherwise.
- The `else` block fills that gap: "if this is true, do this - otherwise, do that."
- Real-life comparison: a restaurant host.
  1. If a table is free, the host seats you immediately.
  2. Otherwise, the host puts your name on the waiting list.
  3. One of these two things always happens.

**Syntax:**
```python
if condition:
    # runs when condition is True
else:
    # runs when condition is False
```

**Example - voting eligibility with else:**
```python
age = 17

if age >= 18:
    print("You are old enough to vote!")
    print("Have you registered to vote yet?")
else:
    print("Sorry, you are too young to vote.")
    print("Please register to vote as soon as you turn 18!")
```
- `age` is `17`, so the condition fails and the `else` block runs instead.
- Unlike a plain `if`, this structure always produces some output - one branch or the other always runs.

**Real-time application:**
- A login page checks the password.
  1. If it matches, the user is sent to their dashboard.
  2. If not, an error message is shown.
- Exactly one of these two outcomes always happens.

---

## 4. elif Statement

**Concept:**
- Sometimes there are more than two possible outcomes.
- `elif` (short for "else if") chains several conditions together.
- Python checks them in order, runs the **first** one that is `True`, then skips all the rest.
- Real-life comparison: an amusement park ticket counter with different prices for different age groups - more than a simple yes/no, there are several price bands to check in sequence.

**Syntax:**
```python
if condition_1:
    # runs if condition_1 is True
elif condition_2:
    # runs if condition_1 is False AND condition_2 is True
elif condition_3:
    # runs if condition_1 and condition_2 are False AND condition_3 is True
else:
    # runs if none of the above were True
```

**Example - amusement park pricing:**
- Under 4 years old: free
- 4 to 17 years old: $5
- 18 to 64 years old: $10
- 65 and older: $5 (senior rate)

```python
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 5
elif age < 65:
    price = 10
else:
    price = 5

print("Your admission cost is $" + str(price) + ".")
```
- `age` is `12`.
- Step 1: Python checks `age < 4` → `False`.
- Step 2: Python checks `age < 18` → `True` → sets `price = 5`.
- Step 3: All remaining checks are skipped automatically, even though some might technically also be true.

**elif chain vs. multiple independent if statements (important interview point):**

- In an `if-elif-else` chain, only **one** block ever runs - the first one whose condition is `True`:
```python
requested_toppings = ['mushrooms', 'extra cheese']

if 'mushrooms' in requested_toppings:
    print("Adding mushrooms.")
elif 'extra cheese' in requested_toppings:
    print("Adding extra cheese.")   # never runs here,
                                     # because the first condition already matched
```

- If you need **every** true condition to trigger its own action, use separate, independent `if` statements instead:
```python
requested_toppings = ['mushrooms', 'extra cheese']

if 'mushrooms' in requested_toppings:
    print("Adding mushrooms.")
if 'extra cheese' in requested_toppings:
    print("Adding extra cheese.")   # this DOES run, because it is a separate if
```

> **Interview tip:** Use an `if-elif-else` chain when exactly one outcome should happen (assigning a single grade or price). Use a series of plain `if` statements when several independent things might all need to happen at once (adding several pizza toppings).

---

## 5. Nested Conditional Statements

**Concept:**
- A nested conditional statement is an `if` (or `if-else`) placed **inside** another `if` block - a decision inside a decision.
- Real-life comparison: withdrawing cash from an ATM happens in stages, and each stage only matters if the previous one succeeded.
  1. Is the card valid? If not, stop here.
  2. If the card is valid, is the PIN correct? If not, stop here.
  3. If the PIN is correct, is the balance sufficient? If not, stop here.
  4. Only if all three checks pass, dispense the cash.

**Example:**
```python
card_valid = True
pin_correct = True
balance = 5000
withdraw_amount = 2000

if card_valid:
    if pin_correct:
        if balance >= withdraw_amount:
            print("Please collect your cash.")
        else:
            print("Insufficient balance.")
    else:
        print("Incorrect PIN.")
else:
    print("Invalid card.")
```

**How this runs, step by step:**
1. Check `card_valid` → `True` → enter the outer block.
2. Check `pin_correct` → `True` → enter the next block.
3. Check `balance >= withdraw_amount` → `5000 >= 2000` → `True`.
4. Print "Please collect your cash."

> **Caution:** Nesting `if` statements three, four, or more levels deep makes code hard to read and debug. If this starts happening, combine conditions with `and` / `or`, or move the logic into a separate function.

**Flatter alternative** (behaves the same for the success case):
```python
if card_valid and pin_correct and balance >= withdraw_amount:
    print("Please collect your cash.")
else:
    print("Transaction failed.")
```

---

## 6. Practical Examples

**Example 1: Grade calculator (elif chain)**
```python
marks = 76

if marks >= 90:
    grade = "A"
elif marks >= 75:
    grade = "B"
elif marks >= 60:
    grade = "C"
elif marks >= 40:
    grade = "D"
else:
    grade = "Fail"

print("Grade:", grade)
```

**Example 2: Leap year checker (nested logic with and/or)**
- Rule: a year is a leap year if it is divisible by 4, but not by 100 - unless it is also divisible by 400.
```python
year = 2024

if year % 4 == 0:
    if (year % 100 != 0) or (year % 400 == 0):
        print(year, "is a leap year.")
    else:
        print(year, "is NOT a leap year.")
else:
    print(year, "is NOT a leap year.")
```

**Example 3: Simple login system (nested if)**
```python
stored_username = "admin"
stored_password = "python123"

entered_username = "admin"
entered_password = "python123"

if entered_username == stored_username:
    if entered_password == stored_password:
        print("Login successful. Welcome!")
    else:
        print("Incorrect password.")
else:
    print("Username not found.")
```

**Example 4: A preview of algorithms - binary search through a phone directory**

- Think about an old-fashioned paper phone directory, with names listed alphabetically.
- To find a name, you do not start at page 1 and read every page. Instead:
  1. Open the directory roughly in the **middle**.
  2. If the name you want comes **before** that page alphabetically, ignore the entire second half of the book and repeat the process only on the first half.
  3. If the name comes **after** that page, ignore the first half and repeat only on the second half.
  4. Keep halving the remaining pages until the name is found (or there are no pages left to check).
- That repeated decision - "is it here, before, or after?" - is exactly how **binary search** works, built entirely out of an `if / elif / else` check repeated again and again:

```python
def binary_search(directory, name):
    low, high = 0, len(directory) - 1

    while low <= high:
        mid = (low + high) // 2

        if directory[mid] == name:
            return mid          # found the name
        elif directory[mid] < name:
            low = mid + 1       # search the right half only
        else:
            high = mid - 1      # search the left half only

    return -1                   # name not found in the directory
```

- We will cover binary search and other algorithms in full detail in a later lesson.
- Key takeaway for now: conditional statements are the decision-making engine underneath even advanced algorithms.

---

## 7. Common Errors and Best Practices

**Common errors:**
1. **Missing colon at the end of the condition line**
   - Wrong: `if age > 18`
   - Fix: `if age > 18:`
2. **Using `=` instead of `==`**
   - Wrong: `if age = 18:`
   - Fix: `if age == 18:`
3. **Inconsistent indentation**
   - Wrong: mixing tabs and spaces, or using a different number of spaces within the same block
   - Fix: use 4 spaces consistently for every level of indentation
4. **Comparing floating-point numbers directly**
   - Wrong: `if result == 0.3:` (floating-point math can produce tiny rounding errors)
   - Fix: `if abs(result - 0.3) < 1e-9:`
5. **Comparing a boolean to True/False explicitly**
   - Unnecessary: `if is_valid == True:`
   - Better: `if is_valid:`
6. **Placing `elif` or `else` in the wrong order**
   - `elif` and `else` must always come directly after an `if` block (or another `elif`); `else` must always be last in the chain.
7. **Expecting every elif to be checked**
   - Once one branch in an `if-elif-else` chain is `True`, Python skips all the remaining checks - even if more than one condition happens to be true.

**Best practices:**
1. Use an `if-elif-else` chain when exactly one outcome should happen; use separate `if` statements when more than one action might need to run independently.
2. Keep nesting shallow - generally no more than two or three levels. Combine conditions with `and` / `or`, or move logic into a function, instead of stacking many nested `if` blocks.
3. Follow PEP 8 style: 4 spaces per indentation level, no tabs, and keep lines under about 80 characters.
4. Use "truthy" and "falsy" values directly: an empty list, empty string, `0`, and `None` are all treated as `False`, so `if my_list:` is cleaner than `if len(my_list) > 0:`.
5. Use a ternary (conditional) expression for short, simple if-else assignments:
```python
status = "Adult" if age >= 18 else "Minor"
```

> **Interview tips:**
> 1. Python had no built-in `switch` statement for a long time; an `if-elif-else` chain or a dictionary lookup was the traditional substitute. Python 3.10 introduced `match-case`, which works similarly to a switch statement in other languages.
> 2. Falsy values in Python include: `0`, `0.0`, `None`, `False`, empty string `""`, empty list `[]`, empty dictionary `{}`, and empty tuple `()`. Everything else is truthy.
> 3. Be ready to explain, with an example, why an `if-elif-else` chain only runs one branch while a series of plain `if` statements can run several.
> 4. Be ready to explain why `if x == True:` is considered bad style compared to `if x:`.

---

## Quick Revision Summary

1. `if condition:` - runs a block only when the condition is `True`; otherwise does nothing.
2. `if condition: ... else: ...` - runs one of exactly two blocks, depending on whether the condition is `True` or `False`.
3. `if ... elif ... elif ... else:` - checks conditions in order and runs only the first matching block; use when exactly one outcome should occur.
4. Nested `if` - an `if` placed inside another `if`, used for step-by-step checks where each step depends on the one before it; keep this shallow.
5. Multiple independent `if` statements (no `elif`) - use when more than one condition might be true and each one needs its own action.
6. Ternary expression `x if condition else y` - a compact one-line version of a simple if-else, best for short assignments.

---

## What's Next

1. Next lesson: loops (`for` and `while`), which let Python repeat actions - the natural next step after learning how Python makes single decisions.
2. After that: functions, data structures, and eventually algorithms like the binary search example previewed above.
3. Feel free to upload the book you mentioned, or let me know if you'd like to continue straight to the next topic.
