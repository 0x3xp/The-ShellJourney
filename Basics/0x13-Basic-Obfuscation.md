# Basic Obfuscation

---

## Module Overview

Obfuscation is the process of making data or code difficult to understand at first glance while still keeping it functional and reversible.

In this module, students will learn:

- What obfuscation is
- Why obfuscation is used
- The difference between obfuscation and encryption
- How ASCII encoding works
- How to manipulate characters in Bash
- How to implement character shifting
- How XOR obfuscation works
- How to reverse obfuscation techniques
- How to debug obfuscated scripts
- How obfuscation is used in CTF-style challenges

This module prepares students for the Final Practical CTF Challenge.

---

# 1. What is Obfuscation?

Obfuscation means deliberately making something unclear or harder to understand.

In programming, obfuscation is commonly used to:

- Hide sensitive strings
- Prevent casual inspection of logic
- Protect simple intellectual property
- Add challenge elements (such as in CTF competitions)
- Reduce readability without changing functionality

Important:

Obfuscation is NOT encryption.

| Obfuscation | Encryption |
|-------------|------------|
| Simple hiding | Secure protection |
| Easily reversible | Requires proper key management |
| Educational / lightweight | Cryptographically secure |
| Not secure against experts | Designed to resist attacks |

In this course, obfuscation is used strictly for learning purposes.

---

# 2. Understanding ASCII

ASCII (American Standard Code for Information Interchange) assigns numeric values to characters.

Examples:

A → 65  
B → 66  
a → 97  
0 → 48  
- → 45  

Understanding ASCII is essential because obfuscation techniques often manipulate character codes directly.

---

## 2.1 Converting Character to ASCII

```bash
#!/bin/bash

char="A"
ascii=$(printf "%d" "'$char")
echo "ASCII value: $ascii"
```

---

## 2.2 Converting ASCII to Character

```bash
#!/bin/bash

ascii=65
char=$(printf "\\$(printf '%03o' $ascii)")
echo "Character: $char"
```

Explanation:

- `%d` converts character to decimal
- `%03o` converts decimal to octal
- `\octal` converts octal to character

---

# 3. Character Shift Obfuscation (Caesar Style)

Character shifting works by increasing or decreasing ASCII values by a fixed number.

Encoding rule:

new_character = original_character + shift_value

Decoding rule:

original_character = encoded_character - shift_value

---

## 3.1 Encoding Example

```bash
#!/bin/bash

original="HELLO"
shift=3
encoded=""

for ((i=0; i<${#original}; i++)); do
    char=${original:$i:1}
    ascii=$(printf "%d" "'$char")
    new_ascii=$((ascii + shift))
    encoded+=$(printf "\\$(printf '%03o' $new_ascii)")
done

echo "Encoded: $encoded"
```

Output:
KHOOR

---

## 3.2 Decoding Example

```bash
#!/bin/bash

encoded="KHOOR"
shift=3
decoded=""

for ((i=0; i<${#encoded}; i++)); do
    char=${encoded:$i:1}
    ascii=$(printf "%d" "'$char")
    new_ascii=$((ascii - shift))
    decoded+=$(printf "\\$(printf '%03o' $new_ascii)")
done

echo "Decoded: $decoded"
```

Output:
HELLO

---

# 4. XOR Obfuscation

XOR is a bitwise operator represented in Bash as:

```
^
```

Key property:

value ^ key ^ key = value

This means applying XOR twice with the same key returns the original value.

This makes XOR perfect for reversible obfuscation.

---

# 5. XOR Encoding (Storing ASCII Values)

Instead of storing characters directly, we can store obfuscated ASCII values in an array.

## Example

```bash
#!/bin/bash

original="FLAG-TEST"
key=42
encoded_values=()

for ((i=0; i<${#original}; i++)); do
    char=${original:$i:1}
    ascii=$(printf "%d" "'$char")
    xor=$((ascii ^ key))
    encoded_values+=($xor)
done

echo "Encoded ASCII values:"
echo "${encoded_values[@]}"
```

This outputs a list of numbers.

---

# 6. XOR Decoding

```bash
#!/bin/bash

encoded_values=(108 102 107 109 7 126 111 121 126)
key=42
decoded=""

for val in "${encoded_values[@]}"; do
    orig=$((val ^ key))
    decoded+=$(printf "\\$(printf '%03o' $orig)")
done

echo "Decoded string: $decoded"
```

Important:
The same key must be used for decoding.

---

# 7. Storing Hidden Flags in Scripts

Instead of writing:

```bash
flag="FLAG-SECRET"
```

We store:

```bash
flag_values=(108 102 107 109 ...)
```

This prevents someone from instantly reading the flag by opening the file.

They must understand:
- Arrays
- Loops
- XOR
- ASCII conversion

This is useful in CTF-style challenges.

---

# 8. Debugging Obfuscated Scripts

When debugging:

1. Check variable names carefully
2. Verify array names
3. Ensure the correct key is used
4. Add temporary echo statements inside loops
5. Confirm arithmetic operations

Example debugging technique:

```bash
echo "Current value: $val"
echo "After XOR: $orig"
```

---

# 9. Mini Lab 1 – User Input Shift

Task:

Write a script that:

1. Prompts user for input
2. Applies shift value 5
3. Prints encoded result
4. Decodes it back to original

Requirements:

- Must use loop
- Must use ASCII conversion
- Must use arithmetic operations

---

# 10. Mini Lab 2 – XOR Practice

Task:

1. Store ASCII values of a secret string inside an array
2. XOR them using key 13
3. Decode and print final string

Goal:

Understand XOR symmetry and array handling.

---

# 11. Debugging Challenge

The following script contains errors.

Fix it and reveal the hidden flag.

```bash
#!/bin/bash

flag_values=(108 102 107 109 7 94 88 89 88 93)
key=42
decoded=""

for value in "${flag_value[@]}"; do
    orig=$((value ^ keys))
    decoded+=$(printf "\\$(printf '%03o' $orig)")
done

echo "Flag: $decoded"
```

Students must:

- Fix incorrect array name
- Fix incorrect variable name
- Ensure correct XOR logic
- Successfully decode flag

---

# 12. Common Mistakes

Students often:

- Forget to use same key for decoding
- Mistype array variable names
- Confuse decimal and octal conversions
- Forget quotes around array expansion
- Misplace braces in arithmetic expansion

Always test small pieces of code first.

---

# 13. Security Considerations

Basic obfuscation:

- Is NOT secure encryption
- Can be reversed by skilled analysts
- Is intended only for lightweight protection or educational purposes

Real encryption requires cryptographic libraries.

---

# 14. Final Practical Preparation

This module directly prepares students for the Final CTF Challenge.

In the final challenge:

- Students receive a broken script
- Script includes:
  - Variables
  - Arrays
  - Functions
  - Conditions
  - Loops
  - XOR obfuscation
  - Logical errors
- Students must debug and extract hidden flag
- Flag unlocks final Google Form exam

This ensures understanding instead of memorization.

---

# 15. Learning Outcomes

After completing this module, students will be able to:

- Explain what obfuscation is
- Differentiate obfuscation from encryption
- Convert characters to ASCII and back
- Implement character shift encoding/decoding
- Implement XOR encoding/decoding
- Debug obfuscated scripts
- Extract hidden information from structured code
- Prepare for CTF-style challenges

---

# End of Module
