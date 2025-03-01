# ShieldPass

ShieldPass is a secure local password manager. There are two versions: MFA-based and USB-based. 

- ShieldPass MFA -- our most updated version of ShieldPass -- requires MFA via authenticator application.
- ShieldPass USB requires an external USB to unlock your passwords -- requiring a physical key to unlock.

## Disclaimer

ShieldPass MFA is intended for secure local management of your sensitive credentials. The overall security depends on the strength of your master password and proper safeguarding of your backup MFA secret. Always follow best practices for password and data security.

---
---

# ShieldPass MFA

ShieldPass MFA is a secure, local password manager that protects your sensitive credentials with state-of-the-art encryption and enforced multi-factor authentication (MFA). All data is stored locally, ensuring that your information never leaves your device.

---

## Features

- **Local Data Security:** No external servers—everything is stored securely on your device.
- **Layered Encryption:** Combines multiple cryptographic methods to protect your data.
- **Multi-Factor Authentication (MFA):** Adds an extra security layer via time-based one-time passwords (TOTP).
- **Secure Backups & File Deletion:** Uses encrypted ZIP archives and secure deletion routines to prevent data recovery.

---

## Encryption & Security Details

### MFA Secret Encryption
- **Algorithm:** AES in Galois/Counter Mode (GCM)
- **Key Derivation:** Uses the scrypt key derivation function with strong parameters.
- **Process:**
  1. A random salt is generated.
  2. The master password (converted to a secure byte array) is processed with scrypt to derive a key.
  3. The MFA secret is encrypted using AES-GCM, which produces a nonce, an authentication tag, and the ciphertext.
  4. The final encrypted payload is composed of salt, nonce, tag, and ciphertext, then base64 encoded for storage.

### Data Encryption (User Credentials)
- **Algorithm:** ChaCha20-Poly1305
- **Key Derivation:** Uses scrypt with stronger parameters.
- **Process:**
  1. The MFA secret (after being base32-decoded) is used with scrypt to derive the encryption key.
  2. A nonce is generated.
  3. User data is encrypted using ChaCha20-Poly1305.
  4. The encrypted output (salt + nonce + ciphertext) is then base64 encoded.

### Encrypted ZIP Storage
- **Library:** pyzipper (AESZipFile)
- **Encryption:** Uses AES-based encryption (WZ_AES) with LZMA compression.
- **Password Management:**
  - A unique ZIP password is generated using secure random tokens.
  - The password is stored via the keyring module, ensuring it is tied to the user account.
  - Critical configuration files are stored within this encrypted ZIP archive.
  - This creates layered encryption security.

---

## MFA Setup & Verification

- **TOTP Generation:** ShieldPass uses TOTP to generate time-based one-time passwords.
- **QR Code Provisioning:** A QR code is generated for easy setup with authenticator apps (like Google Authenticator or Microsoft Authenticator).

---
---

# ShieldPass USB

- **Password Encryption**: ShieldPass uses the ChaCha20-Poly1305 algorithm, a modern and secure encryption standard, to encrypt your data. This ensures that your passwords and other sensitive information are protected against unauthorized access.
  
- **MFA via T**: The key used to encrypt and decrypt your data is stored on an external USB device. This adds an extra layer of security, ensuring that even if your computer is compromised, your data remains safe as long as the USB key is not connected.

- **File Encryption**: ShieldPass stores its encrypted data in an encrypted folder combining AES encryption and ChaCha20-Poly1305 for added security. This folder acts as the "front door" to your data. Only the external USB key can unlock it.

- **Master Password**: The master password, required to access the application, is securely hashed using the scrypt algorithm with a high work factor, making it resistant to brute-force attacks.

- **User-Friendly Interface**: ShieldPass offers a simple and intuitive interface making it easy to manage your passwords and other sensitive information.

- **Backup Options**: ShieldPass allows you to create local or Discord backups of your encrypted data, ensuring that you always have a secure copy of your passwords available.

- **Automatic Locking**: When the application is closed or the USB key is removed, ShieldPass automatically encrypts your data and then locks it in another encrypted folder, ensuring that your information is always secure.

## Encryption Standards

- **ChaCha20-Poly1305**: Used for encrypting passwords and other sensitive data. This algorithm is known for its speed and security, providing both encryption and integrity verification.
  
- **scrypt**: Used for deriving keys from the master password. scrypt is highly resistant to brute-force attacks due to its memory-intensive design.
  
- **AES Encryption (WZ_AES)**: Used for securing the folders that contain your encrypted data. AES is a widely trusted encryption standard.

---
---

## Author

Developed by [avenyx.io](https://avenyx.io)
