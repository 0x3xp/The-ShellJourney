# Exam Preparation

---

## Module Overview

This module serves as the final preparation before the official exam.

Students must apply all previously learned concepts to:

- Analyze a broken script
- Debug logical and syntax errors
- Understand arrays and loops
- Work with ASCII conversion
- Apply XOR decoding
- Extract a hidden flag

The extracted flag will be required to access the final exam.

---

## Objective

By completing this module, students will:

- Demonstrate understanding of Bash fundamentals
- Apply debugging techniques
- Decode obfuscated content
- Prove practical competency before attempting the final exam

This ensures that students truly understand the course content.

---

## Instructions

1. Carefully analyze the script below.
2. Identify all errors.
3. Fix the script.
4. Run the corrected script.
5. Extract the flag.
6. Use the flag to unlock the final exam form.

You must not modify the encoded values or key.
You must only correct logical and syntax issues.

---

## Broken Script (CTF Challenge)

```bash
#!/bin/bash

# XOR Decode Challenge
# Only encoded values are visible

key=42

encoded_values=(
26 114 25 114 115 26 127 121 26
70 124 25 110 123 126 123 97 98 99
18 19 28 28 29 29 26 29 29 14 98
66 110 25 105 25 72
)

decoded=""

for valu in "${encode_values[@]}"; do
    original=$((vale ^ key))
    decode+=$(printf "\\$(printf '%03o' $original)")
done

echo "Flag: $decoded"
```

---

## What This Script Contains

The script includes:

- Variables
- Arrays
- A function
- A conditional statement
- A loop
- XOR obfuscation
- ASCII conversion
- Logical errors

Students must identify and correct:

- Incorrect array reference
- Incorrect variable names
- Incorrect key reference
- Incorrect final output variable

---

## Debugging Guide (Hints)

- Check variable names carefully
- Compare array names
- Verify arithmetic expressions
- Confirm function logic
- Ensure correct echo variable

Do not change the encoded numbers.
Do not change the key.
Only fix broken logic.

---

## Expected Outcome

When correctly fixed and executed, the script will reveal:

```
FLAG-EXAM
```

(This is an example format — your actual flag may vary.)

---

## Why This Is Required

This preparation module ensures:

- Students cannot directly access the exam
- Students must demonstrate practical understanding
- AI copy-paste answers become less effective
- Students gain real debugging experience

---

## After Extracting the Flag

1. Open the Final Exam Google Form.
2. Enter the flag in the first required field.
3. If the flag is correct, you may proceed with the exam.
4. If incorrect, access will be denied.

---

## Learning Outcomes

After completing this module, students will be able to:

- Debug real Bash scripts
- Apply XOR decoding logic
- Understand ASCII transformations
- Analyze structured code
- Extract hidden information from scripts
- Demonstrate readiness for final evaluation

---

# End of Module
