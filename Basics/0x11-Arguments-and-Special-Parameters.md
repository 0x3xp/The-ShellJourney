# Arguments and Special Parameters in Bash

When running a Bash script, you can provide **arguments** (inputs) directly after the script's name. These arguments can be accessed and used inside the script. Additionally, Bash provides **special parameters**, which are predefined read-only variables useful for managing arguments, process IDs, and command status.

---

# 1. Passing Arguments to a Script

Arguments are values provided to a script at runtime. You can pass as many arguments as you need, separated by spaces.

## Syntax

```bash
./script.sh arg1 arg2 arg3 ... argN
```

## Example

```bash
#!/bin/bash

echo "First argument: $1"
echo "Second argument: $2"
echo "Third argument: $3"
```

Run the script:

```bash
./script.sh apple banana cherry
```

Output:

```
First argument: apple
Second argument: banana
Third argument: cherry
```

---

# 2. Special Parameters

Bash provides **predefined variables** that allow you to access arguments, process IDs, and command statuses easily.

| Parameter | Description |
|-----------|-------------|
| `$#`      | Number of arguments passed to the script |
| `$0`      | Name of the script |
| `$1`, `$2`, … | First, second, … argument passed to the script |
| `$*`      | All arguments passed to the script as a single string |
| `$@`      | All arguments passed to the script as an array (preserves quoting) |
| `$!`      | PID of the last background process |
| `$?`      | Exit status of the last executed command |
| `$_`      | Last argument of the previous command |
| `$$`      | PID of the current shell |

---

## Example – Using Special Parameters

```bash
#!/bin/bash

echo "Number of arguments passed: $#"
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments (using \$*): $*"
echo "All arguments (using \$@): $@"
echo "PID of current shell: $$"

# Run a command in background
sleep 10 &
echo "PID of last background process: $!"

# Last argument of previous command
echo "Last argument of previous command: $_"
```

Run the script:

```bash
./script.sh apple banana cherry
```

Example Output:

```
Number of arguments passed: 3
Script name: ./script.sh
First argument: apple
Second argument: banana
All arguments (using $*): apple banana cherry
All arguments (using $@): apple banana cherry
PID of current shell: 12345
PID of last background process: 12346
Last argument of previous command: cherry
```

---

# 3. Notes

1. `$*` treats all arguments as a single string, while `$@` preserves each argument as a separate element when quoted: `"$@"`.  
2. `$?` is useful for checking if the last command succeeded (`0` = success, any other number = error).  
3. Use `$$` for generating temporary filenames or unique process tracking.  
4. `$_` is helpful in scripts to reference the last argument of the previous command without retyping it.  

---

# Mini Practice Tasks

1. Write a script that prints all arguments using a loop and `$@`.  
2. Write a script that prints its own script name and PID.  
3. Write a script that checks if at least 2 arguments are provided using `$#`.  
4. Run a background command inside a script and print its PID using `$!`.  

---

# Summary

- `$1`, `$2`, … `$N` – Access individual arguments.  
- `$*` – All arguments as a single string.  
- `$@` – All arguments as an array.  
- `$#` – Number of arguments.  
- `$0` – Script name.  
- `$?` – Exit status of last command.  
- `$$` – PID of the current shell.  
- `$!` – PID of last background process.  
- `$_` – Last argument of previous command.  

Mastering arguments and special parameters allows you to write flexible and dynamic scripts that can handle input from the user or other programs.
