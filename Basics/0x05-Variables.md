# Variables in Shell Scripting

A variable is a named container used to store data. In shell scripting, variables allow you to store values such as numbers, text, file paths, command output, and more.

Instead of repeating the same value multiple times in a script, you store it once in a variable and reuse it when needed.

---

# Variable Naming Rules

Variable names must follow specific rules:

## Allowed Characters
- Letters: `a-z`, `A-Z`
- Numbers: `0-9`
- Underscore: `_`

## Naming Restrictions
- Must start with a letter or underscore
- Cannot start with a number
- Cannot contain special characters (except `_`)
- No spaces allowed

---

## Valid Variable Names

```bash
variable
_variable2
variable123
USER_NAME
```

## Invalid Variable Names

```bash
2_var      # Starts with a number
!VAR1      # Special character not allowed
$VAR2      # Special character not allowed
my var     # Contains space
```

---

# Defining Variables

Syntax:

```bash
variable_name=value
```

⚠️ Important: No spaces around `=`.

Correct:

```bash
number=10
name="Lucy"
path="/home/user/Desktop"
```

Incorrect:

```bash
number = 10   # This will cause an error
```

---

# Accessing Variables

To use a variable, prefix it with `$`.

Example:

```bash
#!/bin/bash

name="Jacky"
animal="Monkey"

echo "Name: $name"
echo "Animal: $animal"
```

Output:

```
Name: Jacky
Animal: Monkey
```

---

# Using Curly Braces for Clarity

When combining variables with text, use braces:

```bash
file="report"
echo "${file}.txt"
```

This avoids ambiguity.

---

# Command Substitution

Variables can store command output.

```bash
current_date=$(date)
echo "Today's date is: $current_date"
```

Alternative (older syntax):

```bash
current_date=`date`
```

Modern `$( )` syntax is recommended.

---

# Arithmetic with Variables

Use arithmetic expansion:

```bash
a=5
b=3
sum=$((a + b))

echo "Sum: $sum"
```

---

# Deleting Variables

Use `unset` to remove a variable.

```bash
#!/bin/bash

name="Jacky"
echo "Name: $name"

unset name
echo "Variable removed"

echo "Name: $name"
```

After `unset`, the variable has no value.

---

# Read-Only Variables

To prevent modification, mark a variable as readonly.

```bash
#!/bin/bash

pi=3.14
readonly pi

echo $pi

pi=5   # This will cause an error
```

Once marked as readonly, the value cannot change.

---

# Types of Variables

There are three main categories in shell scripting.

---

## 1. Local Variables

Local variables exist only in the current shell session or script.

```bash
name="Joe"
```

They are not accessible to child processes unless exported.

---

## 2. Environment Variables

Environment variables are available to child processes and programs started from the shell.

To create one:

```bash
export PROJECT="ShellCourse"
```

Check it:

```bash
echo $PROJECT
```

Common example:

```bash
export PATH="/usr/local/bin:$PATH"
```

This modifies the system's command search path.

View all environment variables:

```bash
printenv
```

---

## 3. Shell Variables (Built-in Variables)

These are automatically set by the shell.

Examples:

```bash
echo $PWD      # Current directory
echo $HOME     # Home directory
echo $SHELL    # Active shell path
echo $USER     # Current user
echo $?        # Exit status of last command
echo $$        # Current process ID
```

---

# Special Variables

Shell provides special-purpose variables.

## Exit Status

```bash
ls
echo $?
```

`$?` stores the exit code of the previous command.
- `0` = success
- Non-zero = error

---

## Script Arguments

If a script receives arguments:

```bash
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"
echo "Number of arguments: $#"
```

Run:

```bash
./script.sh apple banana
```

Output:

```
First argument: apple
Second argument: banana
All arguments: apple banana
Number of arguments: 2
```

---

# Variable Scope Inside Functions

Example:

```bash
#!/bin/bash

function demo() {
    local message="Inside function"
    echo $message
}

demo
echo $message   # Will be empty
```

Using `local` restricts the variable to the function.

---

# Default Values for Variables

You can provide fallback values:

```bash
echo ${username:-Guest}
```

If `username` is not set, it prints `Guest`.

---

# Checking if a Variable Exists

```bash
if [ -z "$name" ]
then
    echo "Variable is empty"
fi
```

- `-z` → True if empty
- `-n` → True if not empty

---

# Best Practices

- Use meaningful variable names
- Use uppercase for environment variables
- Quote variables when printing:

Correct:

```bash
echo "$name"
```

Prevents unexpected behavior with spaces.

---

# Mini Practice Tasks

1. Create a variable storing your name and print it.
2. Store the current directory using `pwd` into a variable.
3. Create a readonly variable and attempt to modify it.
4. Write a script that prints the number of arguments passed.

---

# Summary

In this module, you learned:

- How to define and access variables
- Naming rules and restrictions
- Command substitution
- Arithmetic operations
- Removing variables
- Readonly variables
- Local vs environment variables
- Built-in shell variables
- Script arguments
- Variable scope and best practices

Variables are essential for building dynamic and intelligent shell scripts. Mastering them allows you to control data flow and automate complex tasks efficiently.
