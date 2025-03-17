# Using PGP Encryption in Apple Mail

## 1. Generating a PGP Key Pair

Before using PGP encryption in Apple Mail, you need to generate a PGP key pair.

### Steps to Generate a PGP Key Pair
1. Install **GnuPG** (GPG) if you haven't already:
   ```sh
   brew install gnupg
   ```
2. Generate a new key pair:
   ```sh
   gpg --full-generate-key
   ```
3. Follow the prompts to:
   - Select key type (**RSA and RSA** recommended)
   - Choose a key size (4096 bits recommended)
   - Set an expiration date
   - Enter your name and email address
   - Set a strong passphrase
4. List your generated keys:
   ```sh
   gpg --list-keys
   ```
   Note the key ID of your new key.
5. Export your public key:
   ```sh
   gpg --armor --export your-key-id > public-key.asc
   ```
6. Export your private key (for backup, store securely!):
   ```sh
   gpg --armor --export-secret-key your-key-id > private-key.asc
   ```

## 2. Installing and Configuring GPG Suite for Apple Mail

1. Download and install [GPG Suite](https://gpgtools.org/).
2. Open **GPG Keychain** and import your generated key if it's not listed:
   ```sh
   gpg --import public-key.asc
   gpg --import private-key.asc
   ```
3. Open **Apple Mail**, go to **Mail** > **Settings** > **GPG Mail**.
4. Ensure your key is selected under **Default Key**.

## 3. Using PGP Encryption in Apple Mail

### Sending an Encrypted Email
1. Compose a new email in **Apple Mail**.
2. Ensure the recipient’s PGP public key is imported into your keychain:
   ```sh
   gpg --import recipient-public-key.asc
   ```
3. Click the **lock icon** in the message window to enable encryption.
4. If the recipient has a PGP key, Apple Mail will encrypt the email.
5. Click **Send**.

### Receiving and Decrypting an Email
1. When receiving a PGP-encrypted email, open it in **Apple Mail**.
2. Enter your passphrase when prompted to decrypt the message.

## 4. Publishing Your PGP Public Key
To allow others to send you encrypted emails, publish your PGP public key:

### Keyservers
Upload your key to a public keyserver:
```sh
 gpg --send-keys --keyserver keyserver.ubuntu.com your-key-id
```

### Personal Website
You can also publish your `public-key.asc` file on your personal website and share the URL.

### Email Signature
Include your public key fingerprint in your email signature:
```
PGP Fingerprint: ABCD 1234 EFGH 5678 IJKL 9012 MNOP 3456 QRST 7890
Public Key: https://yourwebsite.com/your-public-key.asc
```

## 5. Revoking a PGP Key
If you need to revoke your key (e.g., lost key, compromised key):
1. Generate a revocation certificate:
   ```sh
   gpg --output revoke.asc --gen-revoke your-key-id
   ```
2. Upload the revocation certificate to the keyserver:
   ```sh
   gpg --send-keys --keyserver keyserver.ubuntu.com your-key-id
   ```
3. Inform your contacts to stop using your revoked key.

## Conclusion
By setting up PGP encryption in Apple Mail, you enhance your email security and ensure privacy in communications. Make sure to securely back up your private key and periodically refresh your encryption setup.

---

For additional information, refer to the [GPG Tools documentation](https://gpgtools.org/) and [GNU Privacy Handbook](https://www.gnupg.org/gph/en/manual.html).
