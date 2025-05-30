# 🔐 Secure Communication with RSA and AES (Cryptography)

## Developers: Mohamed & Alaa

## 📖 Project Overview

This project simulates a secure communication protocol between two users, Mohamed and Alaa, using a hybrid encryption scheme that combines **asymmetric** and **symmetric cryptography**.

### 🎯 Objectives:
- Simulate the secure exchange of symmetric keys using RSA.
- Encrypt and decrypt a private message using AES.
- Digitally sign the message to ensure authenticity.
- Verify the signature to ensure the message was not tampered with.

### 🧠 How It Works:

1. **Key Generation**  
   Each user generates a pair of RSA keys (private and public). Public keys are exchanged manually.

2. **Secure Key Exchange (Asymmetric Encryption)**  
   - Mohamed generates a random 128-bit AES key fragment and encrypts it with Alaa’s RSA public key.
   - Alaa does the same and encrypts his AES fragment with Mohamed’s public key.
   - Each party decrypts the received fragment using their private RSA key.

3. **Session Key Derivation (SHA-256)**  
   The final AES session key is generated by hashing both fragments:
   ```python
   session_key = SHA256(Mohamed_random + Alaa_random)[:16]
   ```

4. **Message Encryption (Symmetric AES)**
   Mohamed encrypts a secret message using the session key with AES in EAX mode, which ensures both confidentiality and integrity.

5. **Digital Signature**
   Mohamed signs the original message with his private RSA key. This signature proves the message's authenticity.

6. **Decryption and Verification**
   Alaa decrypts the AES-encrypted message and verifies the digital signature using Mohamed’s public RSA key.

### 💡 Why Hybrid Encryption?

* **RSA** is used for secure key exchange and digital signatures (asymmetric).
* **AES** is used for fast and secure message encryption (symmetric).
* This mirrors real-world secure protocols like HTTPS and end-to-end encrypted messaging apps.

---

## 🛠️ Technologies Used

* **Language:** Python 3.9+
* **Library:** [PyCryptodome](https://pycryptodome.readthedocs.io/en/latest/)
* **Platform:** Google Colab / Jupyter Notebook

---

## 📁 Repository Structure

```
├── Mohamed_Encryption.ipynb       # Mohamed's notebook: encryption + signing
├── Alaa_Decryption.ipynb          # Alaa's notebook: decryption + signature verification
```

---

## 🚀 How to Run

1. Clone this repo or open both notebooks in Google Colab.
2. Alaa starts by running **`Alaa_Decryption.ipynb`** to:

   * Generate RSA keys.
   * Share `alaa_pub.pem` and `encrypted_alaa_key.bin` with Mohamed.
3. Mohamed runs **`Mohamed_Encryption.ipynb`** to:

   * Generate his RSA key.
   * Load Alaa's public key and encrypted part.
   * Create and send encrypted message and signature to Alaa.
4. Alaa runs his notebook again to:

   * Decrypt the message.
   * Verify the digital signature from Mohamed.

---

## ✅ Output Example

```bash
Signature valid.
Decrypted message: MohamedID202201647
```

---

## 📦 Requirements

Install dependencies using pip:

```bash
pip install pycryptodome
```

---
