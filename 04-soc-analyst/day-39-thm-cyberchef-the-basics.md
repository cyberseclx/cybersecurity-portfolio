# Day 39 – TryHackMe CyberChef: The Basics

## Room Details

- **Platform:** TryHackMe
- **Learning path:** Cyber Security 101 → Defensive Security Tooling
- **Room:** CyberChef: The Basics
- **Day:** 39
- **Status:** Completed (100%)
- **Estimated room time:** 60 minutes

## Learning Objectives

- Explain what CyberChef is and how it supports security analysis.
- Navigate the Operations, Recipe, Input, and Output areas.
- Build and modify a CyberChef recipe.
- Understand why the order of operations matters.
- Use common encoding, decoding, extraction, and transformation operations.
- Distinguish encoding, encryption, and hashing.
- Use Magic as a starting point while validating its suggestions manually.
- Handle potentially sensitive or malicious data safely.

## What Is CyberChef?

CyberChef is a browser-based data-transformation and analysis tool. It provides many small operations that can be combined into a repeatable workflow called a **recipe**.

Security analysts can use it to:

- Decode encoded text.
- Convert data between formats.
- Extract indicators such as URLs or IP addresses.
- Calculate hashes.
- Inspect or transform suspicious strings.
- Decrypt data when the correct algorithm, key, and parameters are known.
- Reproduce a sequence of analysis steps consistently.

CyberChef is a useful analysis aid, but its output still needs to be interpreted and validated by the analyst.

## Main Interface Areas

| Area | Purpose |
|---|---|
| **Operations** | Searchable collection of functions such as From Base64, From Hex, URL Decode, XOR, and Extract URLs. |
| **Recipe** | Ordered list of operations applied to the input. |
| **Input** | Original text, bytes, or other data to be processed. |
| **Output** | Result produced after the recipe is executed. |

The basic data flow is:

```text
Input → Operation 1 → Operation 2 → Operation 3 → Output
```

Each operation receives the result of the previous operation. This makes the order of a recipe essential.

## Working With Recipes

A recipe is a sequence of operations placed in the Recipe area.

Typical workflow:

1. Place the provided data in the Input area.
2. Search for the required operation.
3. Drag the operation into the Recipe area.
4. Configure its parameters if necessary.
5. Review the Output area.
6. Add another operation if the result has another transformation layer.
7. Rearrange, disable, or remove operations to test the logic.
8. Record the final recipe and interpretation.

Generic example:

```text
Encoded input → From Base64 → URL Decode → Readable output
```

Reversing the two operations may fail or produce a different result because the output of one step becomes the input of the next.

## Bake and Auto Bake

- **Bake** runs the current recipe when the analyst chooses to execute it.
- **Auto Bake** automatically updates the output when the input, recipe, or settings change.

Auto Bake is convenient for small inputs. Manual baking can provide more control when the input is large or the recipe is resource-intensive.

## Common Operations

| Operation | Purpose |
|---|---|
| **From Base64** | Decodes Base64-encoded data. |
| **To Base64** | Encodes data using Base64. |
| **From Hex** | Converts hexadecimal representation back into bytes or text. |
| **To Hex** | Represents input data in hexadecimal form. |
| **URL Decode** | Reverses percent-encoding used in URLs. |
| **URL Encode** | Converts characters into a URL-safe encoded representation. |
| **ROT13** | Applies a fixed letter substitution; applying ROT13 twice restores the original text. |
| **XOR** | Combines data with a key using the XOR operation. |
| **Magic** | Suggests possible transformations based on the input. |
| **Extract URLs** | Finds URL-like strings in the supplied data. |
| **Extract IP addresses** | Finds IP-address patterns in the supplied data. |
| **Strings** | Extracts printable character sequences from data. |
| **Defang URL** | Converts an active-looking URL into a safer form for reporting or sharing. |

Operation names such as **From Base64** describe the direction of the conversion:

```text
From Base64 = decode Base64 data
To Base64   = encode data as Base64
```

## Encoding, Encryption, and Hashing

These concepts serve different purposes and should not be treated as interchangeable.

| Concept | Main purpose | Reversible? | Secret required? |
|---|---|---|---|
| **Encoding** | Represent data in a compatible format. | Yes | No |
| **Encryption** | Protect confidentiality. | Yes, with the correct key and parameters | Yes |
| **Hashing** | Produce a fixed-size digest for comparison or integrity checks. | Not designed to be reversed | No secret is required for a normal hash |

### Encoding

Base64, hexadecimal, and URL encoding are representations, not security controls. Anyone who recognizes the format can normally decode the data.

### Encryption

Encryption transforms plaintext into ciphertext using an algorithm and cryptographic material. Correct decryption may require:

- The algorithm or cipher mode.
- The correct key.
- An initialization vector or nonce.
- Padding and input/output format details.

Seeing unreadable text does not by itself prove that the data is encrypted; it may be encoded, compressed, hashed, or binary.

### Hashing

A cryptographic hash produces a digest that can help compare or identify data. Analysts may use hashes to check file integrity or pivot to threat-intelligence sources. A matching hash indicates matching input under the same algorithm, but the surrounding context still matters.

## Using Magic Carefully

The **Magic** operation analyzes input and suggests possible transformations. It can be helpful when the format is unknown, but its suggestion is not proof.

A safe workflow is:

1. Review the structure and character set of the input.
2. Run Magic to generate possible interpretations.
3. Inspect the suggested operations and confidence.
4. Rebuild or verify the proposed recipe manually.
5. Confirm whether the output is structurally and contextually meaningful.
6. Preserve the original input and document the chosen steps.

Do not accept readable output automatically as correct. Validate it against the investigation context.

## Recognizing Common Data Clues

| Observation | Possible interpretation | Next check |
|---|---|---|
| Letters, numbers, `+`, `/`, and possible `=` padding | Base64 | Try From Base64 and validate the result. |
| Pairs of characters from `0–9` and `a–f` | Hexadecimal | Check length and try From Hex. |
| Sequences such as `%2F` or `%3A` | URL encoding | Try URL Decode. |
| Readable letters shifted consistently | ROT-style substitution | Test the suspected rotation. |
| Mixed or unreadable binary data | Compression, encryption, or another binary format | Inspect file signatures and context before choosing an operation. |

These are clues only. Similar-looking data can have a different meaning.

## Layered Decoding Workflow

Suspicious data may contain several transformation layers. Analyze it one layer at a time:

```text
Preserve original → Identify likely format → Apply one operation → Inspect result → Repeat if justified
```

At each stage, record:

```text
Input format:
Operation used:
Parameters:
Result:
Reason for the next step:
```

This prevents random trial-and-error and makes the analysis reproducible.

## Defensive Security Use Cases

CyberChef can support investigations involving:

- Encoded command lines or PowerShell content.
- URL-encoded web requests.
- Obfuscated phishing links.
- Indicators embedded in logs or alerts.
- Hexadecimal or Base64 data in scripts.
- Hash generation for file comparison.
- Extraction and defanging of URLs before reporting.
- Converting timestamps, character encodings, or byte formats.

A CyberChef result should be correlated with the original alert, log source, endpoint evidence, network activity, and investigation timeline.

## Safe Analysis Workflow

1. Confirm that the data and investigation are authorized.
2. Preserve the original input before transforming it.
3. Avoid submitting confidential or personal data to an unapproved public service.
4. Prefer an approved or locally hosted CyberChef instance for sensitive material.
5. Treat suspicious links and extracted commands as potentially dangerous.
6. Do not click, browse to, or execute decoded content.
7. Apply one justified operation at a time.
8. Validate the output using context and another source of evidence.
9. Save the recipe or document every operation and parameter.
10. Defang malicious indicators before sharing them in reports.

## Practical Reporting Model

Every practical should end with:

```text
What I checked:
The original input, its visible structure, and the sequence of CyberChef operations used.

What I found:
The transformed or extracted data, stated without executing or visiting suspicious content.

What it means:
How the result relates to the alert, log, file, user, host, or investigation timeline.

What I would do next:
The next validation step, related log source, endpoint check, escalation, or containment action required.
```

## Mistakes to Avoid

- Treating Base64 or hexadecimal encoding as encryption.
- Using **To Base64** when the task requires **From Base64**.
- Applying operations in the wrong order.
- Randomly stacking operations until readable text appears.
- Assuming that Magic always identifies the correct recipe.
- Losing the original input during analysis.
- Executing a decoded command or opening an extracted URL.
- Uploading sensitive organizational data to an unapproved service.
- Reporting an extracted indicator without investigation context.
- Publishing room answers, credentials, target details, flags, or sensitive raw output.

## Retention Checks

- Explain what CyberChef is and why a SOC analyst may use it.
- Identify the Operations, Recipe, Input, and Output areas.
- Explain why recipe order changes the result.
- Distinguish Bake from Auto Bake.
- Distinguish encoding, encryption, and hashing.
- Explain the difference between From Base64 and To Base64.
- Describe how Magic should be used and validated.
- Name several useful extraction or decoding operations.
- Explain how to analyze layered data reproducibly.
- State how to handle decoded URLs and commands safely.
- Describe what you checked, found, concluded, and would do next.

## Evidence Boundary

This note records concepts and methods learned in a guided TryHackMe room. It does not claim production CyberChef, malware-analysis, or SOC experience. Exercise answers, credentials, target details, flags, and raw output are intentionally excluded.

## Status

- TryHackMe room: **Completed – 100%**
- Portfolio note: **Prepared**
