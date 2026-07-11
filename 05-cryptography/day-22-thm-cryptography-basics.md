# Day 22 - THM Cyber Security 101: Cryptography Basics

## Block

**Clockify:** `D22-B02 | THM Cyber Security 101 | Cryptography Basics`  
**Project:** `CS Sprint | THM Labs`

## Room

**Path:** Cyber Security 101 → Cryptography → Cryptography Basics  
**Status:** Completed

## Learning Objectives

This room covered the foundation of cryptography:

- Cryptography key terms
- Importance of cryptography
- Plaintext and ciphertext
- Caesar cipher and historical ciphers
- Symmetric encryption
- Asymmetric encryption
- Basic cryptographic math

---

## 1. Why Cryptography Matters

Cryptography is used to protect communication and data.

It helps provide:

```text
Confidentiality = only authorized people can read the data
Integrity = data has not been changed
Authentication = proving identity
Non-repudiation = sender cannot deny the action later
```

Real-world examples:

```text
HTTPS = encrypted web browsing
SSH = encrypted remote login
VPN = encrypted tunnel
Online banking = encrypted transactions
Messaging apps = encrypted communication
Password storage = hashing/salting
```

Without cryptography, attackers may be able to read, modify, or impersonate communication.

---

## 2. Plaintext, Ciphertext, Encryption, and Decryption

```text
Plaintext = original readable message
Ciphertext = encrypted unreadable message
Encryption = plaintext converted into ciphertext
Decryption = ciphertext converted back into plaintext
Cipher = algorithm/method used for encryption/decryption
Key = secret value used with the cipher
```

Memory:

```text
Plaintext + Cipher + Key = Ciphertext
Ciphertext + Cipher + Key = Plaintext
```

Example:

```text
Plaintext: hello
Ciphertext: khoor
```

This can happen with a Caesar cipher shift of 3.

---

## 3. Caesar Cipher

Caesar cipher is a historical cipher where each letter is shifted by a fixed number.

Example with shift 3:

```text
A → D
B → E
C → F
cat → fdw
```

Weakness:

```text
Caesar cipher is weak because there are only a small number of possible shifts.
An attacker can brute force it by trying every shift.
```

Important term:

```text
Brute force = trying all possible keys/passwords/shifts until the correct one works.
```

---

## 4. Symmetric Encryption

Symmetric encryption uses the same key for encryption and decryption.

```text
Same key encrypts
Same key decrypts
```

Examples:

```text
AES
DES
3DES
```

Strength:

```text
Fast
Useful for encrypting large amounts of data
```

Weakness:

```text
Key sharing problem
Both sides need the same secret key safely
```

Real-world use:

```text
Used for bulk data encryption after secure key exchange.
```

Memory:

```text
Symmetric = same key
```

---

## 5. Asymmetric Encryption

Asymmetric encryption uses two keys:

```text
Public key
Private key
```

Public key:

```text
Can be shared with anyone.
```

Private key:

```text
Must be kept secret.
```

Examples:

```text
RSA
ECC
Diffie-Hellman style key exchange concepts
```

Used for:

```text
Key exchange
Digital signatures
Certificates
Authentication
Secure communication setup
```

Memory:

```text
Asymmetric = public/private key pair
```

---

## 6. Symmetric vs Asymmetric

```text
Symmetric encryption:
- Same key
- Fast
- Good for large data
- Has key sharing problem

Asymmetric encryption:
- Public/private key pair
- Slower
- Good for key exchange, signatures, certificates
- Solves safe key exchange problem
```

Important real-world idea:

```text
Many systems use both.
Asymmetric cryptography helps exchange or protect a key.
Symmetric cryptography then encrypts the actual bulk data.
```

---

## 7. Basic Cryptographic Math

### Modulo

Modulo means remainder after division.

```text
10 mod 3 = 1
```

Because:

```text
3 goes into 10 three times = 9
Remainder = 1
```

Used in many cryptographic calculations.

---

### XOR

XOR compares bits.

```text
Same bits = 0
Different bits = 1
```

Truth table:

```text
0 XOR 0 = 0
0 XOR 1 = 1
1 XOR 0 = 1
1 XOR 1 = 0
```

Used in many encryption operations.

---

### Prime Numbers

A prime number is divisible only by 1 and itself.

Examples:

```text
2, 3, 5, 7, 11, 13
```

Prime numbers are important in public key cryptography such as RSA.

---

## 8. Key Terms To Remember

```text
Cryptography = protecting information using mathematical techniques

Plaintext = readable original data

Ciphertext = encrypted unreadable data

Encryption = converting plaintext into ciphertext

Decryption = converting ciphertext back into plaintext

Cipher = encryption/decryption method

Key = value used by cipher

Symmetric encryption = same key

Asymmetric encryption = public/private key pair

Caesar cipher = shift-based historical cipher

Brute force = trying all possible keys

Modulo = remainder after division

XOR = same bits 0, different bits 1
```

---

## 9. Why This Matters For Cybersecurity

Cryptography appears in:

```text
HTTPS / TLS
SSH
VPN
Wi-Fi security
Password hashing
Digital certificates
Kerberos
JWT tokens
Secure file transfer
Malware analysis
Web application security
OSCP enumeration and exploitation
```

A junior pentester or SOC analyst does not need deep mathematics at the beginning, but must understand what cryptography is protecting and where weak crypto can cause risk.

---

## 10. Weak Areas To Revise

```text
Symmetric vs asymmetric encryption
Public key vs private key
Encryption vs hashing
Modulo
XOR
Digital signatures
Certificates
Key exchange
```

Some of these will be covered more deeply in the next rooms:

```text
Public Key Cryptography Basics
Hashing Basics
```

---

## 11. Quick Self-Test

```text
1. What is plaintext?
2. What is ciphertext?
3. What is encryption?
4. What is decryption?
5. What is a cipher?
6. What is a key?
7. What is Caesar cipher?
8. Why is Caesar cipher weak?
9. What is symmetric encryption?
10. What is asymmetric encryption?
11. What is the difference between public key and private key?
12. Why is symmetric encryption faster?
13. What problem does asymmetric encryption help solve?
14. What is modulo?
15. What is XOR?
16. Why are prime numbers important in cryptography?
```
