# ShieldPass

ShieldPass is a secure and efficient password manager designed to protect your sensitive data by leveraging external USB storage for key management and layered encryption. ShieldPass ensures that your passwords and other sensitive information are encrypted using strong encryption algorithms and are only accessible when the correct USB key is connected.

## Features

- **Password Encryption**: ShieldPass uses the ChaCha20-Poly1305 algorithm, a modern and secure encryption standard, to encrypt your data. This ensures that your passwords and other sensitive information are protected against unauthorized access.
  
- **External Key Management**: The key used to encrypt and decrypt your data is stored on an external USB device. This adds an extra layer of security, ensuring that even if your computer is compromised, your data remains safe as long as the USB key is not connected.

- **File Encryption**: ShieldPass stores its encrypted data in an encrypted folder combining AES encryption and ChaCha20-Poly1305 for added security. This folder acts as the "front door" to your data. Only the external USB key can unlock it.

- **Master Password**: The master password, required to access the application, is securely hashed using the scrypt algorithm with a high work factor, making it resistant to brute-force attacks.

- **User-Friendly Interface**: ShieldPass offers a simple and intuitive interface making it easy to manage your passwords and other sensitive information.

- **Backup Options**: ShieldPass allows you to create local or Discord backups of your encrypted data, ensuring that you always have a secure copy of your passwords available.

- **Automatic Locking**: When the application is closed or the USB key is removed, ShieldPass automatically encrypts your data and then locks it in another encrypted folder, ensuring that your information is always secure.

## Encryption Standards

- **ChaCha20-Poly1305**: Used for encrypting passwords and other sensitive data. This algorithm is known for its speed and security, providing both encryption and integrity verification.
  
- **scrypt**: Used for deriving keys from the master password. scrypt is highly resistant to brute-force attacks due to its memory-intensive design.
  
- **AES Encryption (WZ_AES)**: Used for securing the folders that contain your encrypted data. AES is a widely trusted encryption standard.

ShieldPass combines these encryption technologies to provide a robust and secure environment for managing your passwords and sensitive data.
