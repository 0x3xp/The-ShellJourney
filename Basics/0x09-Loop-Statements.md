# Loop Statements in Bash

Loops allow you to execute commands repeatedly until a condition is met. Bash supports several loop types:

- `while` loop  
- `for` loop  
- `until` loop  

Two control keywords are used in loops:

- `break` – exits the current loop immediately.  
- `continue` – skips the current iteration and proceeds to the next one.

---

# 1. `while` Loop

The `while` loop executes commands **as long as a condition is true**. When the condition becomes false, the loop terminates.

## Syntax

```bash
while [ condition ]; do
    # commands to execute
done
```

## Example

```bash
#!/bin/bash

counter=1

while [ $counter -le 5 ]; do
    echo "Counter value: $counter"
    counter=$((counter + 1))
done
```

Output:

```
Counter value: 1
Counter value: 2
Counter value: 3
Counter value: 4
Counter value: 5
```

---

## Using `break` and `continue` with `while`

```bash
#!/bin/bash

counter=1

while [ $counter -le 5 ]; do
    if [ $counter -eq 3 ]; then
        echo "Skipping 3"
        counter=$((counter + 1))
        continue
    fi
    
    if [ $counter -eq 5 ]; then
        echo "Breaking at 5"
        break
    fi

    echo "Counter: $counter"
    counter=$((counter + 1))
done
```

Output:

```
Counter: 1
Counter: 2
Skipping 3
Counter: 4
Breaking at 5
```

---

# 2. `for` Loop

The `for` loop iterates over a **list of items**, which can be an array, a sequence of numbers, or filenames.

## Syntax

```bash
for var in item1 item2 ... itemN; do
    # commands
done
```

## Example – Iterating over strings

```bash
#!/bin/bash

for name in Alice Bob Charlie; do
    echo "Hello, $name!"
done
```

Output:

```
Hello, Alice!
Hello, Bob!
Hello, Charlie!
```

## Example – Iterating over a range of numbers

```bash
#!/bin/bash

for i in {1..5}; do
    echo "Number: $i"
done
```

Output:

```
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```

## Example – Iterating over an array

```bash
#!/bin/bash

fruits=("Apple" "Banana" "Cherry")

for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done
```

Output:

```
Fruit: Apple
Fruit: Banana
Fruit: Cherry
```

---

# 3. `until` Loop

The `until` loop executes commands **as long as a condition is false**. It is the opposite of `while`.

## Syntax

```bash
until [ condition ]; do
    # commands
done
```

## Example

```bash
#!/bin/bash

counter=1

until [ $counter -gt 5 ]; do
    echo "Counter value: $counter"
    counter=$((counter + 1))
done
```

Output:

```
Counter value: 1
Counter value: 2
Counter value: 3
Counter value: 4
Counter value: 5
```

---

# Best Practices

1. Quote variables inside conditions to prevent errors: `[ "$var" -eq 5 ]`.  
2. Use `continue` to skip unwanted iterations, and `break` to exit loops early.  
3. For fixed sequences, prefer `for` loops; for unknown-length tasks, prefer `while` or `until`.  
4. Always ensure the loop will eventually terminate to avoid infinite loops.

---

# Mini Practice Tasks

1. Write a `while` loop to print numbers 10 down to 1.  
2. Write a `for` loop to print all elements of an array.  
3. Write an `until` loop that counts up from 1 to 10.  
4. Modify a loop to skip even numbers using `continue`.  
5. Modify a loop to stop when a number greater than 7 is reached using `break`.

---

# Summary

- `while` – executes as long as the condition is true.  
- `for` – iterates over items, arrays, or ranges.  
- `until` – executes as long as the condition is false.  
- `break` – exits a loop immediately.  
- `continue` – skips the current iteration.  

Loops are essential for repetitive tasks, automating processes, and iterating over data in shell scripts.
