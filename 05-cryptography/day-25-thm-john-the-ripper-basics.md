# Day 25 - THM Cyber Security 101: John the Ripper Basics

## Block

**Clockify:** `D25-B01 | THM Cyber Security 101 | John the Ripper Basics`  
**Project:** `CS Sprint | THM Labs`

## Room

**Path:** Cyber Security 101 → Cryptography → John the Ripper: The Basics  
**Status:** Completed

---

## 1. What Is John the Ripper?

John the Ripper is a password/hash cracking tool.

It can be used for:

```text
Basic hashes
Windows authentication hashes
Linux /etc/shadow hashes
Password-protected Zip files
Password-protected RAR files
SSH private key passphrases
```

Important memory:

```text
John does not decrypt hashes.
John guesses passwords, hashes those guesses, and compares the result with the target hash.
```

---

## 2. Basic Terms

```text
Hash = one-way output created from input data/password

Cracking = guessing possible passwords until one creates the same hash

Wordlist = list of possible passwords

Dictionary attack = trying passwords from a wordlist

Brute force = trying all possible combinations

Rule = modifies wordlist words to create more guesses

Hash format/type = tells John how to process the hash
```

Example:

```text
password → hash
John guesses: 123456, password, admin123
If hash(guess) matches target hash, password is found.
```

---

## 3. Basic John Workflow

General pattern:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

If John needs a specific format:

```bash
john --format=<format> --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Show cracked passwords:

```bash
john --show hash.txt
```

List supported formats:

```bash
john --list=formats
```

Search supported formats:

```bash
john --list=formats | grep -i md5
```

---

## 4. Wordlists

Common wordlist:

```text
rockyou.txt
```

Common Kali location:

```bash
/usr/share/wordlists/rockyou.txt
```

If compressed:

```bash
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz
```

Do not repeatedly unzip if the file is already decompressed.

---

## 5. Cracking Basic Hashes

Basic format:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

With explicit format:

```bash
john --format=<format> --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Show result:

```bash
john --show hash.txt
```

Important:

```text
If John cannot detect the hash automatically, use --format.
```

---

## 6. Cracking Windows Authentication Hashes

Windows authentication hashes often involve NTLM / NT hashes.

Common John style:

```bash
john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Memory:

```text
Windows local password hash = NTLM / NT hash concept
```

Important real-world concept:

```text
Sometimes you do not need to crack a Windows hash.
In some situations, pass-the-hash can use the hash directly for authentication.
```

Difference:

```text
Cracking = recover plaintext password
Pass-the-hash = use the hash itself to authenticate
```

---

## 7. Cracking Linux /etc/shadow Hashes

Linux password hashes are stored in `/etc/shadow`.

John often needs `/etc/passwd` and `/etc/shadow` combined.

Tool:

```bash
unshadow passwd.txt shadow.txt > unshadowed.txt
```

Then crack:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
```

Show result:

```bash
john --show unshadowed.txt
```

Memory:

```text
unshadow combines passwd + shadow into a John-readable format.
```

---

## 8. Single Crack Mode

Single crack mode uses available context, such as usernames, to generate password guesses.

Example idea:

```text
username: john
possible guesses: john, John, john123, John2024
```

Command:

```bash
john --single hash.txt
```

Memory:

```text
Single mode uses user/account information to create smarter guesses.
```

---

## 9. Custom Rules

Rules modify wordlist entries to create more guesses.

Example transformations:

```text
password
Password
password1
password123
Password!
```

Purpose:

```text
Rules make dictionary attacks more powerful without needing a huge manual wordlist.
```

---

## 10. Cracking Password-Protected Zip Files

Helper tool:

```bash
zip2john
```

Workflow:

```bash
zip2john file.zip > zip_hash.txt

john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt

john --show zip_hash.txt
```

Memory:

```text
zip2john extracts Zip password hash data into John-readable format.
```

---

## 11. Cracking Password-Protected RAR Files

Helper tool:

```bash
rar2john
```

Workflow:

```bash
rar2john file.rar > rar_hash.txt

john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt

john --show rar_hash.txt
```

Memory:

```text
rar2john extracts RAR password hash data into John-readable format.
```

---

## 12. Cracking SSH Private Key Passphrases

Helper tool:

```bash
ssh2john
```

Workflow:

```bash
ssh2john id_rsa > ssh_hash.txt

john --wordlist=/usr/share/wordlists/rockyou.txt ssh_hash.txt

john --show ssh_hash.txt
```

Important:

```text
This cracks the SSH private key passphrase, not the server password.
```

Memory:

```text
SSH private key passphrase protects the private key file.
If cracked, attacker may be able to use the private key.
```

---

## 13. Helper Tools Summary

```text
zip2john = converts Zip file password data
rar2john = converts RAR file password data
ssh2john = converts SSH private key passphrase data
unshadow = combines passwd + shadow for Linux hash cracking
```

---

## 14. Key Commands To Remember

```bash
john --list=formats

john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

john --format=<format> --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

john --show hash.txt

unshadow passwd.txt shadow.txt > unshadowed.txt

zip2john file.zip > zip_hash.txt

rar2john file.rar > rar_hash.txt

ssh2john id_rsa > ssh_hash.txt
```

---

## 15. Important Concepts

```text
John cracks by guessing, not decrypting.

The correct hash format matters.

Wordlists are used for dictionary attacks.

Rules modify wordlist entries.

Helper tools convert protected files into John-readable hash format.

Cracking a weak password is possible if the password exists in the wordlist or can be generated by rules.

Strong password policies make cracking much harder.
```

---

## 16. Why This Matters For Pentesting

John is useful for:

```text
Cracking weak password hashes
Testing password policy strength
Cracking Linux shadow hashes after privilege escalation
Cracking Windows hashes
Cracking protected archives found during enumeration
Cracking SSH key passphrases
CTF and exam labs
PJPT / CPTS / OSCP foundation
```

Real-world caution:

```text
Only crack hashes in authorized labs, CTFs, or approved security assessments.
```

---

## 17. Weak Areas To Revise

```text
Hash format selection
John --show usage
unshadow workflow
zip2john workflow
rar2john workflow
ssh2john workflow
Single crack mode
Custom rules
Pass-the-hash vs cracking
```

---

## 18. Quick Self-Test

```text
1. What does John the Ripper do?
2. Does John decrypt hashes?
3. What is a wordlist?
4. What is a dictionary attack?
5. What is rockyou.txt?
6. What does john --show do?
7. Why might --format be needed?
8. What does unshadow do?
9. What does zip2john do?
10. What does rar2john do?
11. What does ssh2john do?
12. What is single crack mode?
13. What are custom rules used for?
14. What is the difference between cracking and pass-the-hash?
15. What does ssh2john crack: server password or private key passphrase?
```

---
