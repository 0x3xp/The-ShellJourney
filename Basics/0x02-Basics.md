# Basics – Shell Scripting Foundations

## What Is the Shell?

The shell is a command-line interface that acts as a translator between the user and the operating system. When you type a command, the shell interprets it and communicates with the operating system kernel to execute the requested task.

In simple terms:

User → Shell → Operating System → Output

The shell allows you to:
- Run system commands
- Automate repetitive tasks
- Manage files and processes
- Build scripts to control system behavior

The most common shell on Linux systems is **Bash (Bourne Again Shell)**.

---

# Creating Your First Shell Script

A shell script is simply a text file containing a sequence of commands.

## Step 1: Navigate to a Working Directory

```bash
cd ~/Desktop
```

## Step 2: Create a Script File

Scripts typically use the `.sh` extension.

```bash
touch first_script.sh
```

## Step 3: Make the Script Executable

By default, new files are not executable. Grant execution permission using:

```bash
chmod +x first_script.sh
```

## Step 4: Add Code to the Script

Open the file with a text editor such as `nano`:

```bash
nano first_script.sh
```

Add the following content:

```bash
#!/bin/bash

echo "This is my first shell script."
ls
echo "Script execution completed."
```

### Explanation

- `#!/bin/bash` → Shebang line. It tells the system to use Bash to execute the script.
- `echo` → Prints text to the terminal.
- `ls` → Lists files in the current directory.

## Step 5: Run the Script

```bash
./first_script.sh
```

If everything is correct, the script will:
1. Print a message
2. Display directory contents
3. Print a closing message

---

# Comments in Shell Scripts

Comments improve readability and maintainability. They are ignored during execution.

## Single-Line Comments

Single-line comments begin with `#`.

```bash
# This is a comment
echo "Hello World"
```

## Multi-Line Comments

Bash does not have a true multi-line comment syntax like some languages, but a common workaround is:

```bash
: '
This is a multi-line comment.
Everything inside this block
is ignored by the shell.
'
```

Use comments to:
- Explain logic
- Document decisions
- Clarify complex sections

---

# Variables

Variables store data that can be reused throughout a script.

Bash is dynamically typed, meaning you do not declare variable types.

## Creating Variables

```bash
name="John"
age=25
```

⚠️ Important: Do not leave spaces around the `=` sign.

## Accessing Variables

Use `$` before the variable name:

```bash
echo $name
echo "Age: $age"
```

## Environment Variables

Environment variables are predefined by the system.

View them with:

```bash
printenv
```

Example usage:

```bash
echo $HOME
echo $PATH
```

---

# Comparison Operators

Comparisons are commonly used in conditional statements.

## Integer Comparisons

| Operator | Meaning |
|----------|----------|
| -eq | Equal |
| -ne | Not equal |
| -gt | Greater than |
| -ge | Greater than or equal |
| -lt | Less than |
| -le | Less than or equal |

Example:

```bash
if [ 5 -gt 3 ]
then
    echo "5 is greater than 3"
fi
```

## String Comparisons

| Operator | Meaning |
|----------|----------|
| == | Equal |
| != | Not equal |
| \< | Alphabetically less than |
| \> | Alphabetically greater than |

Example:

```bash
if [ "$name" == "John" ]
then
    echo "Name matches"
fi
```

Note: When using `<` or `>`, they should be escaped inside brackets.

---

# Conditional Statements

Conditional statements allow decision-making in scripts.

## if Statement

```bash
if [ condition ]
then
    # commands
fi
```

Example:

```bash
a=10
b=10

if [ $a -eq $b ]
then
    echo "Values are equal"
fi
```

---

## if-else Statement

```bash
if [ condition ]
then
    # if true
else
    # if false
fi
```

Example:

```bash
a=10
b=20

if [ $a -eq $b ]
then
    echo "Equal"
else
    echo "Not equal"
fi
```

⚠️ Always leave spaces inside `[ ]`.

Correct:
```bash
[ $a -eq $b ]
```

Incorrect:
```bash
[$a -eq $b]
```

---

# Loops

Loops execute a block of code repeatedly.

## While Loop

Executes as long as the condition remains true.

```bash
number=1

while [ $number -lt 5 ]
do
    echo $number
    number=$((number + 1))
done
```

Output:
```
1
2
3
4
```

---

## For Loop

Iterates over a list of values.

```bash
for num in 4 8 12 20 25 30
do
    echo $num
done
```

Output:
```
4
8
12
20
25
30
```

You can also use ranges:

```bash
for i in {1..5}
do
    echo $i
done
```

---

# Summary

In this module, you learned:

- What the shell is and how it works
- How to create and execute shell scripts
- How to use comments
- How to define and access variables
- How to compare values
- How to write conditional statements
- How to use loops

These are the fundamental building blocks of shell scripting. Mastering them will allow you to automate tasks and build more advanced scripts in later modules.
