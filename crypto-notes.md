# Cryptography Notes
**Apex Planet Cybersecurity Internship**

## Symmetric vs Asymmetric Encryption

- **Symmetric** — same key encrypts and decrypts. Fast, used for bulk data. Examples: AES, ChaCha20. Main challenge: securely sharing the key between parties.
- **Asymmetric** — key pair: public key encrypts/verifies, private key decrypts/signs. Slower, used for key exchange and authentication. Examples: RSA, ECC. Solves the key-distribution problem symmetric crypto has.
- **In practice**: TLS uses asymmetric crypto to securely exchange a symmetric session key, then switches to symmetric encryption for the actual data — combining the secure key exchange of asymmetric crypto with the speed of symmetric crypto.

## Hashing

- A one-way function: data → fixed-length digest. Cannot be reversed back to the original data.
- Used for integrity checks, password storage (with salting), and digital signatures.
- **MD5** — 128-bit output, cryptographically broken (collision attacks possible), only suitable for basic checksums, not security.
- **SHA-256** — 256-bit output (SHA-2 family), still considered secure, used widely in TLS, blockchain, and digital signatures.
- Example commands: `sha256sum file.txt`, `md5sum file.txt`

## Digital Certificates & TLS/SSL

- A certificate binds a public key to an identity (domain/organization), signed by a trusted Certificate Authority (CA).
- Simplified TLS handshake:
  1. Client sends a "hello" with supported ciphers.
  2. Server responds with its certificate (containing its public key).
  3. Client verifies the certificate against a trusted CA, then generates a symmetric session key and encrypts it using the server's public key.
  4. Both sides now share a symmetric key and switch to fast symmetric encryption for the rest of the session.
- HTTPS = HTTP running inside a TLS-encrypted tunnel.

## Hands-on: OpenSSL Encrypt/Decrypt (AES-256-CBC)

Demonstrates symmetric encryption end-to-end.

```bash
echo "This is my Apex Planet OpenSSL test file." > secret.txt

# Encrypt
openssl enc -aes-256-cbc -salt -pbkdf2 -in secret.txt -out secret.enc

# Decrypt
openssl enc -d -aes-256-cbc -pbkdf2 -in secret.enc -out decrypted.txt

# Verify
diff secret.txt decrypted.txt   # no output = identical, decryption succeeded
```

**Flow:** Plaintext → AES-256-CBC (symmetric) encryption using a password-derived key (via PBKDF2) → ciphertext (`secret.enc`) → decrypted back to the original plaintext using the same password.

**Evidence captured:** `ls -l secret.txt secret.enc decrypted.txt`, `cat decrypted.txt`, `diff secret.txt decrypted.txt`.

---
*Practiced and documented as part of the Apex Planet Cybersecurity Internship lab.*
