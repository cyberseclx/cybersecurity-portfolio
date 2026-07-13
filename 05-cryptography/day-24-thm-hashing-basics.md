# Day 24 - THM Cyber Security 101: Hashing Basics

## Block

**Clockify:** `D24-B02 | THM Cyber Security 101 | Hashing Basics`  
**Project:** `CS Sprint | THM Labs`

## Room

**Path:** Cyber Security 101 → Cryptography → Hashing Basics  
**Status:** Completed

---

## Learning Objectives

This room covered:

- Hash functions and hash values
- Hash collisions
- Hashing in authentication systems
- Insecure password storage
- Secure password storage using hashes and salts
- Recognising stored hash formats
- Password cracking basics
- Hashing for file integrity checking

---

## 1. What Is Hashing?

A hash function takes input of any size and produces a fixed-size output called a hash value.

```text
Input = any size
Output = fixed-size hash value
```

Example:

```text
Input: 6 GB file
Output: fixed-length hash string
```

Hashing is useful because even a small change in the input should create a very different hash.

---

## 2. Hash Function Properties

Important properties:

```text
Deterministic = same input always gives same hash
Fixed-size output = output length stays the same
One-way = difficult to reverse hash back to original input
Avalanche effect = small input change causes large hash change
Collision = two different inputs produce same hash
```

Important memory:

```text
Hashing is not encryption.
Encryption can be decrypted.
Hashing is one-way.
```

---

## 3. Hashing vs Encryption

```text
Encryption:
- Two-way process
- Can be decrypted with the correct key
- Used for confidentiality

Hashing:
- One-way process
- Cannot be decrypted
- Used for password verification and integrity checking
```

Memory:

```text
Encryption protects secrecy.
Hashing proves matching/integrity.
```

---

## 4. Insecure Password Storage

Bad practice:

```text
Storing passwords in plaintext
```

Why this is dangerous:

```text
If the database leaks, attackers immediately know all user passwords.
```

Better approach:

```text
Store password hashes instead of plaintext passwords.
```

---

## 5. Password Verification With Hashes

Login flow:

```text
1. User enters password.
2. Website hashes the entered password.
3. Website compares that hash with the stored hash.
4. If hashes match, login succeeds.
```

The website does not need to store the real password.

---

## 6. Salted Hashes

A salt is a random value added to the password before hashing.

```text
Password + Salt → Hash
```

Why salt matters:

```text
Same password should not create the same stored hash for every user.
Salt helps defend against rainbow table attacks.
```

Example:

```text
user1 password: password123 + salt1 → different hash
user2 password: password123 + salt2 → different hash
```

---

## 7. Good and Bad Password Hashing

Weak or outdated for password storage:

```text
MD5
SHA1
Plain SHA256 without salt
```

Better password hashing algorithms:

```text
bcrypt
scrypt
Argon2
PBKDF2
```

Reason:

```text
Password hashing should be slow enough to make mass cracking harder.
```

---

## 8. Recognising Hashes

Different hashes often have different lengths and formats.

Common examples:

```text
MD5 = 32 hex characters
SHA1 = 40 hex characters
SHA256 = 64 hex characters
SHA512 = 128 hex characters
```

Linux `/etc/shadow` style identifiers:

```text
$1$ = MD5-based crypt
$5$ = SHA-256 crypt
$6$ = SHA-512 crypt
$2a$ / $2b$ / $2y$ = bcrypt
```

Tools for hash identification:

```text
hashid
hash-identifier
name-that-hash
```

Important:

```text
Hash identification is based on format and length.
It is not always 100% certain.
```

---

## 9. Password Cracking

Password cracking means guessing possible passwords, hashing them, and comparing the result with the target hash.

Important memory:

```text
Cracking does not decrypt the hash.
It guesses passwords until the hash matches.
```

Common tools:

```text
John the Ripper
Hashcat
```

Common attack types:

```text
Dictionary attack = tries passwords from a wordlist
Brute force = tries all possible combinations
Rule-based attack = modifies wordlist words
Example: password → Password123!
```

Common wordlist:

```text
rockyou.txt
```

---

## 10. Hashing for Integrity Checking

Hashing can verify whether a file has changed.

Example flow:

```text
1. Website provides SHA256 hash for a file.
2. User downloads the file.
3. User calculates SHA256 hash locally.
4. If both hashes match, the file is likely unchanged.
```

Important memory:

```text
Same file = same hash
Changed file = different hash
```

Common Linux commands:

```bash
md5sum file.txt
sha1sum file.txt
sha256sum file.txt
sha512sum file.txt
```

Real-world uses:

```text
Verify downloaded ISO files
Check malware samples
Detect file tampering
Compare backups
Verify forensic evidence
```

---

## 11. Key Comparisons

### Hashing vs Encryption

```text
Hashing = one-way
Encryption = reversible with key
```

### Hashing vs Encoding

```text
Hashing = one-way integrity/matching
Encoding = reversible format conversion
```

### Plaintext Password vs Hashed Password

```text
Plaintext password = actual password stored directly
Hashed password = hash stored, not the real password
```

### Hash vs Salted Hash

```text
Hash = password hashed directly
Salted hash = password + random salt hashed together
```

### Dictionary Attack vs Brute Force

```text
Dictionary attack = uses wordlist
Brute force = tries all possible combinations
```

### Hash Cracking vs Decryption

```text
Hash cracking = guessing until hash matches
Decryption = reversing ciphertext with key
```

---

## 12. Why Hashing Matters For Cybersecurity

Hashing appears in:

```text
Password storage
Linux /etc/shadow
Web application login systems
File integrity checks
Malware analysis
Forensics
Digital evidence validation
CTF rooms
John the Ripper
Hashcat
SOC investigations
```

A junior pentester or SOC analyst should understand whether a value is:

```text
a plaintext password
a hash
a salted hash
an encrypted value
an encoded value
```

---

## 13. Commands To Remember

```bash
md5sum file.txt
sha1sum file.txt
sha256sum file.txt
sha512sum file.txt
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
hashcat -m <mode> hash.txt wordlist.txt
```

Do not run cracking commands blindly. First identify:

```text
Hash type
Correct hash mode
Correct wordlist
Correct tool
```

---

## 14. Weak Areas To Revise

```text
Hashing vs encryption
Hashing vs encoding
Salt and rainbow table defense
Hash identification
John vs Hashcat basics
Dictionary attack vs brute force
Integrity checking commands
Linux /etc/shadow hash format
```

---

## 15. Quick Self-Test

```text
1. What is a hash function?
2. What is a hash value?
3. Why is hashing one-way?
4. What is a collision?
5. Why is plaintext password storage bad?
6. How does password verification work with hashes?
7. What is a salt?
8. Why does salt help?
9. Why are MD5 and SHA1 weak for password storage?
10. What is hash cracking?
11. Why is cracking not the same as decrypting?
12. What is John the Ripper used for?
13. What is Hashcat used for?
14. What is rockyou.txt?
15. How can hashing verify file integrity?
16. Which command calculates SHA256 hash of a file?
```

---
