# Conditional Statements in Bash

Conditional statements allow your scripts to make decisions based on specific conditions. By using them, you can control the flow of your program and execute different commands depending on the situation.

Bash supports several types of conditional statements:

- `if` statement  
- `if-else` statement  
- `if-elif-else` statement  
- `case` statement (similar to switch-case in other languages)  

---

# 1. The `if` Statement

Executes a command only when a condition is true.

## Syntax

```bash
if [ condition ]; then
    # commands to execute
fi
```

> ⚠️ Note: Always include spaces after `[` and before `]`.  

## Example

```bash
#!/bin/bash

number=15

if [ $number -gt 10 ]; then
    echo "The number is greater than 10."
fi
```

Output:

```
The number is greater than 10.
```

---

# 2. The `if-else` Statement

Provides an alternative set of commands if the condition is false.

## Syntax

```bash
if [ condition ]; then
    # commands if true
else
    # commands if false
fi
```

## Example

```bash
#!/bin/bash

number=5

if [ $((number % 2)) -eq 0 ]; then
    echo "The number is even."
else
    echo "The number is odd."
fi
```

Output:

```
The number is odd.
```

---

# 3. The `if-elif-else` Statement

Used to check multiple conditions in order. Only the first true condition is executed.

## Syntax

```bash
if [ condition1 ]; then
    # commands for condition1
elif [ condition2 ]; then
    # commands for condition2
else
    # commands if none are true
fi
```

## Example

```bash
#!/bin/bash

number=-5

if [ $number -gt 0 ]; then
    echo "The number is positive."
elif [ $number -lt 0 ]; then
    echo "The number is negative."
else
    echo "The number is zero."
fi
```

Output:

```
The number is negative.
```

---

# 4. The `case` Statement

The `case` statement executes commands based on the value of a variable. It is cleaner when handling multiple possible values.

## Syntax

```bash
case variable in
    pattern1)
        commands ;;
    pattern2)
        commands ;;
    ...
    *)
        default commands ;;
esac
```

- `*)` is the default case if no patterns match.  
- Patterns can include multiple values separated by `|`.

## Example

```bash
#!/bin/bash

day="Monday"

case $day in
    Monday)
        echo "It's Monday, the beginning of the week." ;;
    Friday)
        echo "It's Friday, the end of the workweek." ;;
    Saturday|Sunday)
        echo "It's the weekend!" ;;
    *)
        echo "It's a regular day." ;;
esac
```

Output:

```
It's Monday, the beginning of the week.
```

---

# Comparison Operators in Conditionals

| Type           | Operator | Description |
|----------------|----------|------------|
| Integer        | -eq      | Equal |
|                | -ne      | Not equal |
|                | -gt      | Greater than |
|                | -ge      | Greater than or equal |
|                | -lt      | Less than |
|                | -le      | Less than or equal |
| String         | = or == | Equal |
|                | !=       | Not equal |
|                | <        | Less than (alphabetical) |
|                | >        | Greater than (alphabetical) |

> ⚠️ For `<` and `>`, quote them or escape with `\` when used inside `[ ]`.

---

# Logical Operators

- AND: `&&`  
- OR: `||`  
- NOT: `!`  

Example:

```bash
#!/bin/bash

a=10
b=20

if [ $a -lt 15 ] && [ $b -gt 15 ]; then
    echo "Both conditions are true."
fi
```

Output:

```
Both conditions are true.
```

---

# Best Practices

1. Always use spaces around brackets: `[ condition ]`.
2. Quote variables in comparisons to prevent errors: `[ "$var" == "value" ]`.
3. Prefer `case` when checking multiple specific values for readability.
4. Use `elif` instead of nested `if` for clarity.

---

# Mini Practice Tasks

1. Write a script that checks if a number is positive, negative, or zero.  
2. Write a script to determine if a number is divisible by 3, 5, or both.  
3. Create a script that prints a different message for weekdays and weekends using `case`.  
4. Write a script to compare two strings and print which one is alphabetically first.

---

# Summary

- `if` executes commands only if a condition is true.  
- `if-else` provides an alternative when the condition is false.  
- `if-elif-else` handles multiple conditions sequentially.  
- `case` is useful for handling multiple known values cleanly.  
- Conditional statements combined with comparison and logical operators give you powerful control over script flow.
