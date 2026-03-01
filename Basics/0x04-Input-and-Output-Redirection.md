# Input and Output Redirection

When a command runs in Linux, it interacts with three standard data streams:

- **Standard Input (stdin)** → Input to a command
- **Standard Output (stdout)** → Normal output from a command
- **Standard Error (stderr)** → Error messages

By default:
- Input comes from the keyboard
- Output goes to the terminal screen

Redirection allows us to change where input comes from and where output goes.

This is extremely powerful in shell scripting because it allows automation, logging, data processing, and chaining commands together.

---

# Standard Streams Explained

Every process in Linux has three file descriptors:

| Descriptor | Name   | Number |
|------------|--------|--------|
| stdin      | Input  | 0      |
| stdout     | Output | 1      |
| stderr     | Error  | 2      |

We can redirect any of these streams.

---

# Overwrite Redirection

## Redirect Standard Output (`>`)

The `>` operator redirects standard output to a file.

If the file exists, it will be overwritten.

```bash
echo "Hello World" > output.txt
```

Now check the file:

```bash
cat output.txt
```

---

## Redirect Standard Input (`<`)

The `<` operator feeds input into a command from a file instead of the keyboard.

Example:

```bash
cat < output.txt
```

This tells `cat` to take its input from `output.txt`.

---

# Append Redirection

## Append Output (`>>`)

The `>>` operator appends output to a file without removing existing content.

```bash
echo "Second line" >> output.txt
```

Check result:

```bash
cat output.txt
```

This preserves previous data.

---

# Redirecting Errors

Sometimes a command generates errors.

Example:

```bash
ls non_existing_file
```

This produces an error message.

## Redirect Only Errors (`2>`)

```bash
ls non_existing_file 2> error.txt
```

Error messages are now stored in `error.txt`.

---

## Redirect Both Output and Errors

```bash
command > all_output.txt 2>&1
```

Explanation:
- `>` redirects standard output
- `2>&1` redirects error output to wherever stdout is going

Modern shortcut:

```bash
command &> all_output.txt
```

---

# Discarding Output

Sometimes you want to ignore output completely.

Use `/dev/null`:

```bash
command > /dev/null
```

Discard errors:

```bash
command 2> /dev/null
```

Discard everything:

```bash
command > /dev/null 2>&1
```

Very useful in automation scripts.

---

# Here-Document (<<)

A here-document allows you to provide multi-line input directly inside a script.

Syntax:

```bash
command << DELIMITER
text
more text
DELIMITER
```

Example:

```bash
cat << END
This is line 1
This is line 2
END
```

Output:

```
This is line 1
This is line 2
```

---

## Here-Document in Scripts

Example script:

```bash
#!/bin/bash

cat << EOF > config.txt
username=admin
password=secret
port=8080
EOF
```

This creates a file called `config.txt` with predefined content.

Very useful for:
- Auto-generating configuration files
- Automating installations
- Sending input to programs

---

# Here-String (<<<)

A here-string sends a single string as input.

```bash
wc -w <<< "Count these words"
```

This avoids creating a temporary file.

---

# Input and Output Together (Pipes)

Although technically not redirection, pipes are closely related.

The `|` operator sends the output of one command as input to another.

Example:

```bash
ls -l | grep ".txt"
```

This:
1. Lists files
2. Filters only `.txt` files

More example:

```bash
cat access.log | grep "ERROR" | wc -l
```

Counts the number of lines containing "ERROR".

---

# Practical Script Example

Logging command output:

```bash
#!/bin/bash

echo "Script started at $(date)" > script.log

ls /home >> script.log 2>> script.log

echo "Script finished at $(date)" >> script.log
```

This:
- Creates a log file
- Appends command output
- Appends errors if any
- Records timestamps

---

# Overwrite vs Append Summary

| Operator | Function |
|----------|----------|
| >        | Overwrite stdout |
| >>       | Append stdout |
| <        | Redirect stdin |
| 2>       | Redirect stderr |
| &>       | Redirect stdout and stderr |
| <<       | Here-document |
| <<<      | Here-string |

---

# Why Redirection Matters

Redirection allows you to:

- Create logs
- Capture command output
- Suppress unwanted output
- Chain commands
- Automate data processing
- Run non-interactive scripts
- Control program input/output flow

Without redirection, shell scripting would be very limited.

---

# Mini Practice Tasks

1. Redirect the output of `date` into a file called `time.txt`.
2. Append the output of `whoami` to the same file.
3. Redirect errors from `ls /root` into `errors.txt`.
4. Count the number of lines in `/etc/passwd` using input redirection.

---

# Summary

In this module, you learned:

- The concept of stdin, stdout, and stderr
- How to overwrite and append output
- How to redirect input from files
- How to handle error output
- How to use here-documents
- How to discard output safely
- How to combine commands using pipes

Mastering redirection allows you to control data flow in scripts and build powerful automation workflows.
