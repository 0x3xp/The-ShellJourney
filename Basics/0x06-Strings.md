# Strings in Bash

A string is a sequence of characters. In shell scripting, strings are one of the most commonly used data types. They can represent text, file paths, usernames, command output, configuration values, and more.

Bash provides powerful built-in mechanisms for manipulating strings without requiring external tools.

---

# Assigning and Printing Strings

In Bash, variables do not require type declarations. A variable can store text, numbers, or command output.

## Basic Assignment

```bash
name="Alice"
title='Cyber Security'
path=/home/user/Desktop
```

⚠️ No spaces around `=`.

Correct:

```bash
name="Alice"
```

Incorrect:

```bash
name = "Alice"
```

---

## Printing a String

```bash
echo $name
echo "$name"
echo ${name}
```

All are valid, but quoting is recommended:

```bash
echo "$name"
```

Quoting prevents word splitting issues when strings contain spaces.

---

# Understanding Quotes

## Double Quotes `" "`

- Allow variable expansion
- Allow command substitution

```bash
name="Alice"
echo "Hello $name"
```

Output:
```
Hello Alice
```

---

## Single Quotes `' '`

- Treat everything literally
- No variable expansion

```bash
echo 'Hello $name'
```

Output:
```
Hello $name
```

---

# Finding String Length

Use `#` before the variable name.

```bash
title="cybersecurity"
echo ${#title}
```

Output:
```
13
```

This returns the number of characters.

---

# String Concatenation

Strings can be combined in multiple ways.

```bash
first="Cyber"
second="Security"

combined="${first}${second}"
echo "$combined"
```

Output:
```
CyberSecurity
```

You can also add spaces:

```bash
combined="${first} ${second}"
echo "$combined"
```

⚠️ Important clarification:

Using:

```bash
combined="$first $second"
```

is completely valid and safe. The shell does NOT treat `$second` as a command. Quoted concatenation is recommended.

---

# Extracting Substrings

Bash allows slicing strings using parameter expansion.

---

## From Position to End

Syntax:

```bash
${variable:position}
```

Example:

```bash
title="Introduction to Bash Scripting"
echo ${title:7}
```

This prints from index 7 to the end.

Note:
- Indexing starts at 0.

---

## From Position with Specific Length

Syntax:

```bash
${variable:position:length}
```

Example:

```bash
title="Introduction to Bash Scripting"
echo ${title:7:4}
```

This extracts 4 characters starting from position 7.

---

# Negative Indexing (Modern Bash)

In Bash 4.2+, negative offsets count from the end.

```bash
word="cybersecurity"
echo ${word: -8}
```

⚠️ Notice the space before `-8`.

This extracts the last 8 characters.

---

# Removing Substrings (Pattern Matching)

## Remove Shortest Match from Beginning

```bash
file="report.txt"
echo ${file#*.}
```

Removes shortest match before `.`

Output:
```
txt
```

---

## Remove Longest Match from Beginning

```bash
path="/home/user/docs/report.txt"
echo ${path##*/}
```

Output:
```
report.txt
```

Useful for extracting filenames.

---

## Remove from End

```bash
file="report.txt"
echo ${file%.txt}
```

Output:
```
report
```

---

# Replacing Text in Strings

## Replace First Occurrence

```bash
text="I love Linux"
echo ${text/Linux/Bash}
```

Output:
```
I love Bash
```

---

## Replace All Occurrences

```bash
text="admin admin admin"
echo ${text//admin/user}
```

Output:
```
user user user
```

---

# Checking If a String Is Empty

```bash
if [ -z "$name" ]
then
    echo "String is empty"
fi
```

- `-z` → True if empty
- `-n` → True if not empty

---

# Converting Case

## Convert to Uppercase

```bash
word="cyber"
echo ${word^^}
```

Output:
```
CYBER
```

---

## Convert to Lowercase

```bash
word="SECURITY"
echo ${word,,}
```

Output:
```
security
```

---

# Splitting Strings (Using IFS)

Internal Field Separator (IFS) controls word splitting.

Example:

```bash
data="apple,banana,orange"
IFS=',' read -ra fruits <<< "$data"

echo "${fruits[0]}"
echo "${fruits[1]}"
echo "${fruits[2]}"
```

---

# Comparing Strings

```bash
if [ "$a" == "$b" ]
then
    echo "Strings are equal"
fi
```

Not equal:

```bash
if [ "$a" != "$b" ]
then
    echo "Strings are different"
fi
```

Always quote variables during comparisons to prevent errors.

---

# Practical Script Example

```bash
#!/bin/bash

filename="backup_2026.log"

echo "Full filename: $filename"
echo "File extension: ${filename##*.}"
echo "File without extension: ${filename%.*}"
echo "Length of filename: ${#filename}"
```

---

# Mini Practice Tasks

1. Store your full name in a variable and print its length.
2. Extract the last 4 characters from a string.
3. Replace the word "test" with "production" in a variable.
4. Convert a string to uppercase.

---

# Summary

In this module, you learned:

- How to assign and print strings
- The difference between single and double quotes
- How to calculate string length
- How to concatenate strings
- How to extract substrings
- How to remove parts of strings
- How to replace text
- How to compare strings
- How to convert case

String manipulation is a core skill in shell scripting and is heavily used in automation, log processing, configuration handling, and system administration tasks.
