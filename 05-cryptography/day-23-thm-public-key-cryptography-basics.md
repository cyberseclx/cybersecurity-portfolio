# Day 23 - THM Cyber Security 101: Public Key Cryptography Basics

## Block

**Clockify:** `D23-B02 | THM Cyber Security 101 | Public Key Cryptography Basics`  
**Project:** `CS Sprint | THM Labs`

## Room

**Path:** Cyber Security 101 → Cryptography → Public Key Cryptography Basics  
**Status:** Completed

## Learning Objectives

This room covered the basics of public key cryptography and where it is used in real systems.

Topics covered:

- Asymmetric encryption
- RSA
- Diffie-Hellman key exchange
- SSH
- Digital signatures
- SSL/TLS certificates
- PGP and GPG

---

## 1. Security Goals

Public key cryptography helps with several security goals.

```text
Authentication = proving who someone is
Authenticity = proving the message/source is genuine
Integrity = proving data was not changed
Confidentiality = keeping data secret from unauthorized people
```

Simple memory:

```text
Confidentiality = secret
Integrity = unchanged
Authentication = correct identity
Authenticity = genuine source/message
```

Symmetric encryption mainly helps with confidentiality.

Public key cryptography helps with:

```text
Authentication
Authenticity
Integrity
Secure key exchange
Digital signatures
Certificates
```

---

## 2. Public Key and Private Key

Asymmetric cryptography uses two keys:

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

Memory:

```text
Public key = share
Private key = protect
```

---

## 3. RSA

RSA is a public key cryptography algorithm.

It uses:

```text
Public key = (n, e)
Private key = (n, d)
```

Simple memory:

```text
e = encryption/public exponent
d = decryption/private exponent
n = modulus used in both keys
```

The public key is shared openly.

Example:

```text
Bob's public key = (n, e)
Alice uses Bob's public key to encrypt.
Bob uses his private key to decrypt.
```

Important RSA memory:

```text
Public key encrypts.
Private key decrypts.

Private key signs.
Public key verifies.
```

RSA security is based on the difficulty of factoring a very large number created from two large prime numbers.

Simple story:

```text
Public key = lock
Private key = unlock key
```

---

## 4. RSA Example Understanding

In the room example, Bob selected two prime numbers:

```text
p = 157
q = 199
```

Then:

```text
n = p × q
n = 31243
```

Bob selected values for `e` and `d`.

```text
Public key = (31243, 163)
Private key = (31243, 379)
```

Alice needs `e` because it is part of Bob's public key.

Flow:

```text
Bob gives Alice public key: (n, e)
Alice encrypts using: (n, e)
Bob decrypts using: (n, d)
```

Important:

```text
Alice never needs Bob's private key.
Bob never shares d.
```

---

## 5. Diffie-Hellman Key Exchange

Diffie-Hellman allows two parties to create a shared secret over an insecure network.

Important point:

```text
The final shared secret is not directly sent over the network.
```

Used in:

```text
TLS
VPNs
SSH-like secure communication concepts
Secure key exchange
```

Memory:

```text
Diffie-Hellman = shared secret creation
```

Difference from RSA:

```text
RSA = public/private key algorithm
Diffie-Hellman = key exchange method
```

---

## 6. SSH

SSH means Secure Shell.

Purpose:

```text
Encrypted remote login to another machine.
```

SSH uses cryptography for:

```text
Server authentication
Encrypted communication
Password-based login
Key-based login
```

SSH command format:

```bash
ssh user@MACHINE_IP
```

Room credentials:

```text
Username: user
Password: Tryhackme123!
```

---

## 7. SSH Key-Based Login

SSH key login uses a public/private key pair.

Private key:

```text
Stays on your own machine.
Must never be shared.
```

Public key:

```text
Copied to the remote server.
Can be shared.
```

Safe method:

```bash
ssh-keygen
ssh-copy-id user@MACHINE_IP
```

Important SSH files:

```text
id_rsa = private key, keep secret
id_rsa.pub = public key, can be copied to server
authorized_keys = public keys allowed to log in
known_hosts = remembered server identities
```

Memory:

```text
Private key stays with user.
Public key goes to server.
```

Why generate keys on your own machine?

```text
Because the private key should never exist on the remote machine.
Only the public key should be copied to the server.
```

For temporary CTF boxes, the risk is lower, but in real life private keys must be protected.

---

## 8. Digital Signatures

A digital signature proves:

```text
Who signed it
That the data was not changed
```

Simple rule:

```text
Private key signs.
Public key verifies.
```

Digital signatures provide:

```text
Authenticity
Integrity
Non-repudiation
```

Memory:

```text
Signing is not mainly for secrecy.
Signing is for trust and integrity.
```

---

## 9. Certificates

A certificate connects a public key to an identity/domain.

Example:

```text
A certificate proves that a public key belongs to example.com.
```

A certificate contains information such as:

```text
Domain / identity
Public key
Validity period
Issuer / Certificate Authority
CA signature
```

Certificate Authority:

```text
CA = trusted organization that signs certificates.
```

Used in:

```text
HTTPS / TLS
Browser trust
Secure websites
```

Memory:

```text
Certificate = identity + public key + CA signature
```

---

## 10. PGP and GPG

PGP/GPG are used for encrypting and signing files, messages, and emails.

PGP:

```text
Pretty Good Privacy
```

GPG:

```text
GNU Privacy Guard
Open-source implementation of PGP
```

Uses:

```text
Encrypt messages/files for confidentiality
Sign messages/files for authenticity and integrity
```

Memory:

```text
Encrypt = only receiver can read
Sign = receiver can verify sender and integrity
```

---

## 11. High-Priority Comparisons

### Symmetric vs Asymmetric

```text
Symmetric = same key for encryption and decryption
Asymmetric = public/private key pair
```

### Public Key vs Private Key

```text
Public key = can be shared
Private key = must stay secret
```

### Encryption vs Signing

```text
Encryption = confidentiality
Signing = authenticity + integrity
```

### RSA vs Diffie-Hellman

```text
RSA = public key algorithm
Diffie-Hellman = shared secret/key exchange method
```

### Digital Signature vs Certificate

```text
Digital signature = proves data/source was not changed and is genuine
Certificate = binds a public key to an identity/domain
```

### SSH Password Login vs SSH Key Login

```text
Password login = prove identity with password
Key login = prove identity with private key while server stores public key
```

### PGP vs GPG

```text
PGP = encryption/signing system
GPG = open-source implementation of PGP
```

---

## 12. Why This Matters For Cybersecurity

Public key cryptography appears in:

```text
SSH
HTTPS / TLS
SSL/TLS certificates
VPNs
Email encryption
Digital signatures
PGP/GPG
Authentication systems
Secure key exchange
```

For pentesting and SOC work, this helps with understanding:

```text
SSH keys
Certificate warnings
Expired certificates
Weak crypto
Public/private key misuse
TLS configuration issues
Authentication mechanisms
```

---

## 13. Weak Areas To Revise

```text
RSA public key vs private key
Encryption vs signing
Diffie-Hellman key exchange
SSH key-based login
authorized_keys vs known_hosts
Digital signature vs certificate
Certificate Authority role
PGP vs GPG
```

---

## 14. Quick Self-Test

```text
1. What is public key cryptography?
2. What is a public key?
3. What is a private key?
4. In RSA, which key encrypts?
5. In RSA, which key decrypts?
6. In digital signatures, which key signs?
7. In digital signatures, which key verifies?
8. What is Diffie-Hellman used for?
9. What is SSH used for?
10. In SSH key login, where does the private key stay?
11. In SSH key login, what is copied to the server?
12. What is authorized_keys?
13. What is known_hosts?
14. What does a digital signature prove?
15. What does a certificate bind together?
16. What is a Certificate Authority?
17. What is PGP/GPG used for?
18. What is the difference between encryption and signing?
```

---
