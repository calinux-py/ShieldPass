# ShieldPass

**Contents**
1. [ShieldPass Overview](#shieldpass-overview)
2. [ShieldPass MFA](#shieldpass-mfa)
3. [ShieldPass USB](#shieldpass-usb)
4. [Author](#author)

---

## ShieldPass Overview

ShieldPass is a secure local password manager. There are two versions: MFA-based and USB-based. 

- **ShieldPass MFA** — our most updated version of ShieldPass — requires multi-factor authentication via an authenticator application.
- **ShieldPass USB** uses an external USB device as a physical key to unlock your passwords, offering an alternative layer of protection.

---

## Disclaimer

ShieldPass is intended for secure local management of your sensitive credentials. The overall security depends on the strength of your master password and proper safeguarding. Always follow best practices for password and data security.

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
- **Algorithm:** AESZipFile
- **Encryption:** Uses AES-based encryption (WZ_AES) with LZMA compression.
- **Password Management:**
  - A unique ZIP password is generated using secure random tokens.
  - The password is stored via keyring, ensuring it is tied to the user account.
  - Critical configuration files are stored within this encrypted ZIP archive.
  - This creates layered encryption security.

---

## MFA Setup & Verification

- **TOTP Generation:** ShieldPass MFA uses TOTP to generate time-based one-time passwords.
- **QR Code Provisioning:** A QR code is generated for easy setup with authenticator apps (like Google Authenticator or Microsoft Authenticator).

---
---

# ShieldPass USB

ShieldPass USB is our alternative secure, local password manager that, much like ShieldPass MFA, ensures your sensitive credentials are protected using state-of-the-art encryption techniques—but with one key difference. Instead of an authenticator app, ShieldPass USB relies on a physical USB device to serve as the additional authentication factor.

## Features

- **Robust Password Encryption:** Utilizes the ChaCha20-Poly1305 algorithm to encrypt your data, ensuring that your passwords and sensitive information are safeguarded.
- **Physical Key Security:** The encryption key used for both encrypting and decrypting your data is securely stored on an external USB device. This means that even if your computer is compromised, your data remains inaccessible without the USB key.
- **Layered File Encryption:** Data is stored within an encrypted folder that combines AES encryption with ChaCha20-Poly1305. This folder acts as a secure gateway to your information, which can only be unlocked with the USB key.
- **Master Password Protection:** Access to the application requires a master password, which is securely hashed using the scrypt algorithm with a high work factor, making it highly resistant to brute-force attacks.
- **User-Friendly Interface:** An intuitive and simple interface makes managing your passwords and other sensitive data straightforward.
- **Flexible Backup Options:** Offers the ability to create local backups or secure backups via Discord, ensuring you always have a safe copy of your encrypted data.
- **Automatic Locking:** When the application is closed or the USB key is removed, ShieldPass USB automatically re-encrypts and locks your data in a secure folder.

## Encryption & Security Details

- **Encryption Standards:** ShieldPass USB employs the robust ChaCha20-Poly1305 algorithm for encrypting sensitive data. Additionally, AES encryption (WZ_AES) secures the folders containing your data—mirroring the multi-layered security approach seen in ShieldPass MFA.
- **Key Derivation:** The master password is processed using the scrypt algorithm, ensuring that the derived key is highly resistant to brute-force attacks.
- **Physical Authentication:** By requiring a dedicated USB key to store and access the encryption key, ShieldPass USB provides a tangible layer of security that complements its digital encryption methods.

---
---

## Author

Developed by [avenyx.io](https://avenyx.io)
