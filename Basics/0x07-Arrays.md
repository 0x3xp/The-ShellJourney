# Arrays in Bash

When working with multiple values, defining many individual variables is inefficient. Arrays allow you to store multiple values under a single name and access them using indices.

Array indices in Bash start at **0**.

---

# Defining Arrays

There are several ways to define arrays.

---

## 1. Indirect Assignment

Assign a value directly to a specific index.

```bash
arr[0]="Apple"
arr[1]="Banana"
arr[2]="Cherry"
```

---

## 2. Explicit Declaration

Declare an array first, then assign values.

```bash
declare -a fruits
fruits[0]="Apple"
fruits[1]="Banana"
fruits[2]="Cherry"
```

---

## 3. Compound Assignment (Recommended)

Define an array with initial values.

```bash
colors=("Red" "Green" "Blue" "Yellow")
```

Or use explicit indices:

```bash
colors=([0]="Red" [1]="Green" [2]="Blue" [3]="Yellow")
```

---

# Accessing Array Elements

Use the index inside square brackets:

```bash
echo "${colors[0]}"   # Red
echo "${colors[2]}"   # Blue
```

---

# Printing All Elements

Two common syntaxes:

```bash
echo "${colors[@]}"   # Red Green Blue Yellow
echo "${colors[*]}"   # Red Green Blue Yellow
```

- `${array[@]}` treats each element as separate word  
- `${array[*]}` treats all elements as a single word in some contexts  

---

# Printing Elements from a Specific Index

```bash
echo "${colors[@]:2}"   # Blue Yellow
echo "${colors[*]:1}"   # Green Blue Yellow
```

---

# Printing a Range of Elements

```bash
echo "${colors[@]:1:2}"  # Green Blue
```

Syntax:

```
${array[@]:start_index:length}
```

---

# Determining Array Length

```bash
echo "Number of elements: ${#colors[@]}"
```

Output:

```
Number of elements: 4
```

---

# Getting Index of Last Element

```bash
echo "Last element index: $((${#colors[@]} - 1))"
echo "Last element: ${colors[-1]}"  # Bash 4.2+
```

---

# Iterating Over Arrays

### Using `for` loop

```bash
for color in "${colors[@]}"
do
    echo "Color: $color"
done
```

### Using indices

```bash
for i in "${!colors[@]}"
do
    echo "Index $i: ${colors[i]}"
done
```

---

# Adding and Removing Elements

### Adding an element

```bash
colors+=("Purple")
echo "${colors[@]}"   # Red Green Blue Yellow Purple
```

### Removing an element

```bash
unset colors[1]      # Removes "Green"
echo "${colors[@]}"  # Red Blue Yellow Purple
```

---

# Multi-Dimensional Arrays (Simulated)

Bash does not natively support true multi-dimensional arrays, but you can simulate them:

```bash
matrix=([0,0]=1 [0,1]=2 [1,0]=3 [1,1]=4)
echo "${matrix[0,1]}"  # 2
```

---

# Practical Script Example

```bash
#!/bin/bash

arr=("Apple" "Banana" "Blue" "Red" "Yellow" "Blue")

echo "All elements:"
echo "${arr[@]}"

echo "First element: ${arr[0]}"

selected_index=3
echo "Element at index $selected_index: ${arr[$selected_index]}"

echo "Elements from index 2 onwards: ${arr[@]:2}"
echo "Elements from index 1, 3 elements: ${arr[@]:1:3}"
```

Output:

```
All elements:
Apple Banana Blue Red Yellow Blue
First element: Apple
Element at index 3: Red
Elements from index 2 onwards: Blue Red Yellow Blue
Elements from index 1, 3 elements: Banana Blue Red
```

---

# Mini Practice Tasks

1. Create an array containing 5 different programming languages and print all elements.
2. Print the third element of the array.
3. Append a new language to the array and print the updated array.
4. Remove the second element and print the array again.
5. Print elements in a range (e.g., elements 1 to 3).

---

# Summary

In this module, you learned:

- What arrays are and why they are useful
- Different ways to define arrays
- Accessing and printing array elements
- Array length and last element
- Iterating over arrays using loops
- Adding and removing elements
- Simulating multi-dimensional arrays
- Practical usage patterns for scripts

Arrays allow efficient storage and manipulation of multiple values, making your scripts cleaner and more powerful.
