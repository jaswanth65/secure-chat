# Implementation of a Secure Chat Protocol Using Python

## Overview
This project is a simplified implementation of a secure messaging protocol developed using Python. It demonstrates core principles of confidentiality and integrity through the use of manually implemented AES encryption in Counter (CTR) mode and HMAC-SHA256 authentication using Python’s standard library.
The simulator showcases how secure communication can be achieved using symmetric cryptography, ensuring that messages are both encrypted and tamper-proof. Unlike traditional plaintext messaging, this protocol encrypts messages and attaches a cryptographic signature (HMAC) to verify authenticity. The design is modular, reproducible, and suitable for educational demonstrations of secure message flow, tampering detection, and key-based authentication — all without relying on external cryptographic libraries.
## Core Components
**Manual AES-CTR Encryption:** Ensures message confidentiality using a 128-bit symmetric key and a unique nonce.
**HMAC-SHA256 Authentication**: Provides integrity and authenticity using Python’s built-in  and  modules.
**Tampering Detection:** Demonstrates how unauthorized modifications are detected and rejected.
**Interactive CLI:** Allows users to choose between genuine and tampered message flows


## Project Structure
```text
secure-chat/
├── main.py                 # Interactive runner for genuine vs tampered message flow
├── chat/
│   ├── sender.py           # Encrypts and authenticates message
│   └── receiver.py         # Verifies and decrypts message
├── crypto/
│   ├── aes_core.py         # Manual AES-128 block cipher implementation
│   └── ctr_mode.py         # CTR mode logic using aes_core
├── auth/
│   └── hmac_utils.py       # HMAC computation and verification
├── .gitignore              # Excludes pycache, venv, etc.
└── README.md               # Documentation file
```
## Approach

### Genuine Message Flow
1.  **Key Generation:** AES and HMAC keys are randomly generated (16 bytes and 32 bytes respectively).
2.  **Message Encryption:** Plaintext is encrypted using AES-CTR with a random nonce.
3.  **HMAC Computation:** A MAC is computed over `nonce||ciphertext`.
4.  **Secure Message Assembly:** Final message = `nonce + ciphertext + hmac`.
5.  **Receiver Verification:** HMAC is verified before decryption. If valid, message is decrypted and displayed.

### Tampered Message Flow
1.  A byte in the ciphertext is flipped.
2.  Receiver detects HMAC mismatch and rejects the message.

## Challenges & Solutions

### Challenges
* Implementing AES-128 block cipher manually (S-box, key expansion, rounds).
* Constructing CTR mode without built-in libraries.
* Ensuring reproducibility and modular clarity.
* Designing tampering scenarios that trigger HMAC failure.
* Managing byte-level operations and encoding formats.

### Solutions
* Built AES-128 from scratch using FIPS-197 standard (no external libraries).
* Used XOR-based keystream generation for CTR mode.
* Leveraged Python’s built-in  and  for authentication
* Printed all intermediate values (keys, nonce, ciphertext, HMAC) for transparency.
* Created modular files for sender, receiver, and crypto utilities.
* Designed CLI prompt to switch between genuine and tampered flows.

## How to Run

### Step 1: Setup Project Folder
```bash
mkdir secure-chat
cd secure-chat
```
### Step 2: Create and Activate Virtual Environment
```bash
py -m venv venv
venv\Scripts\activate
```
### Step 3: Install Required Package
```bash
pip install cryptography
```
### Step 4: Run the Simulator
```bash
python main.py
```
Choose 1: Genuine secure message flow
Choose 2: Tampered message test

### Sample Input Message: 
```bash
Hello Bob, this is Alice!
```

### Sample Output
```bash
AES Key (Base64): ...
HMAC Key (Base64): ...
Nonce: ...
Ciphertext: ...
HMAC: ...
HMAC Verified
Decrypted Message: Hello Bob, this is Alice!
```
### References
```text
Python cryptography documentation – AES-CTR mode
Python hmac and hashlib modules
RFC 2104 – HMAC: Keyed-Hashing for Message Authentication
```
