# Functions in Bash

A **function** is a reusable block of code that performs a specific task. Functions help make scripts:

- Modular and easier to maintain  
- Readable and organized  
- Reusable for multiple parts of a program  

---

# 1. Defining Functions

## Syntax

```bash
function_name() {
    # commands to execute
}
```

- Function names should start with a letter or underscore.  
- No spaces are allowed around the parentheses.  

## Example

```bash
#!/bin/bash

greetings() {
    echo "Hello!"
}

# Call the function multiple times
greetings
greetings
greetings
```

Output:

```
Hello!
Hello!
Hello!
```

---

# 2. Passing Parameters to Functions

You can pass arguments to a function. Inside the function:

- `$1` – first argument  
- `$2` – second argument  
- `$@` – all arguments  
- `$#` – number of arguments  

## Syntax

```bash
example() {
    echo "Parameter1: $1"
    echo "Parameter2: $2"
}

# Call the function
example 5 10
```

## Example – Math Function

```bash
#!/bin/bash

multiply() {
    result=$(($1 * $2))
    echo "Multiplication Result: $result"
}

multiply 5 8
```

Output:

```
Multiplication Result: 40
```

---

# 3. Returning Values from Functions

Functions can return values using the `return` keyword. **Note:** `return` can only return integer values (0–255). For strings or larger numbers, use `echo` and capture the output.  

## Example – Using `return` for integers

```bash
#!/bin/bash

add_numbers() {
    sum=$(($1 + $2))
    return $sum
}

add_numbers 50 10
echo "Result of addition: $?"
```

Output:

```
Result of addition: 60
```

> ⚠️ `$?` captures the return value of the last executed command or function.  

---

## Example – Returning strings

```bash
#!/bin/bash

greet_user() {
    echo "Hello, $1!"
}

# Capture function output into a variable
message=$(greet_user "Alice")
echo "$message"
```

Output:

```
Hello, Alice!
```

---

# 4. Local vs Global Variables in Functions

- **Global variables**: accessible anywhere in the script.  
- **Local variables**: exist only inside the function (use `local` keyword).  

```bash
#!/bin/bash

my_function() {
    local local_var="I am local"
    global_var="I am global"
    echo "$local_var"
}

my_function
echo "$global_var"   # Accessible
echo "$local_var"    # Not accessible, will be empty
```

Output:

```
I am local
I am global
```

---

# 5. Function Best Practices

1. Keep functions short and focused on one task.  
2. Use descriptive names for readability.  
3. Use `local` for temporary variables to avoid conflicts.  
4. Always document what each function does, its parameters, and return values.  

---

# Mini Practice Tasks

1. Write a function that prints a greeting for a given name.  
2. Write a function that calculates the square of a number passed as a parameter.  
3. Write a function that sums three numbers and returns the result.  
4. Write a function that takes a string as input and prints its length.  

---

# Summary

- Functions group commands into reusable blocks.  
- Parameters can be passed using `$1`, `$2`, … `$@`.  
- Return values are captured using `return` (integers) or `echo` (strings).  
- Use `local` variables to prevent unwanted scope issues.  
- Functions improve modularity, readability, and maintainability of scripts.
