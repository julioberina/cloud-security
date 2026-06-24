# Public-Key Cryptography: The Pragmatic Cheat Sheet

## The Golden Rule
*   **Public Key:** The "Padlock." You can hand it out to anyone. It’s used to **lock** things or **verify** things.
*   **Private Key:** The "Physical Key." You never share it. It’s used to **unlock** things or **prove** identity.

---

## 1. SSH (Accessing EC2)
**Goal:** Authentication (Prove who you are).

*   **How it works:**
    *   **AWS/EC2** keeps your **Public Key** inside the file `~/.ssh/authorized_keys` on the server.
    *   **You** keep the **Private Key** (`.pem` file) on your laptop.
*   **The Logic:** When you connect, your laptop uses the Private Key to "sign" a challenge from the server. The server uses the Public Key to see if the signature is valid.
*   **Security Insight:** This is why "Losing the .pem file" means you are locked out. The server knows what your "padlock" looks like, but you lost the only physical key that fits it.

---

## 2. HTTPS / TLS (Browsing the Web)
**Goal:** Trust + Confidentiality (Ensure I'm talking to the real site and no one is listening).

*   **How it works:**
    *   **The Server** presents a Certificate containing its **Public Key**.
    *   **Your Browser** uses that Public Key to agree on a "Symmetric Session Key" (a temporary password for that specific visit).
*   **The Logic:** The Public Key is used to set up a secure "tunnel." Once the tunnel is built, asymmetric crypto steps aside because it's too slow for big data; symmetric crypto takes over for the actual browsing.
*   **Security Insight:** This is why expired certificates trigger warnings. If the "Public Key" presented doesn't match the one signed by a trusted authority (CA), you might be talking to an impostor.

---

## 3. Digital Signatures (Email / code Signing)
**Goal:** Integrity + Non-repudiation (Prove this hasn't been tampered with).

*   **How it works:**
    *   **The Sender** uses their **Private Key** to "stamp" the document (Signature).
    *   **The Recipient** uses the sender's **Public Key** to check the stamp.
*   **The Logic:** If the document was changed by even one character after being signed, the Public Key check will fail.
*   **Security Insight:** In DevOps, we use this to sign container images or code. If the signature doesn't match, the cloud environment refuses to run the code.

---

## 4. Encryption (Secret Messages)
**Goal:** Confidentiality (Only the target can read this).

*   **How it works:**
    *   **The Sender** uses the **Recipient's Public Key** to lock the message.
    *   **The Recipient** uses their own **Private Key** to unlock it.
*   **The Logic:** Anyone can lock the box, but only the owner of the Private Key can open it.
*   **Security Insight:** This is the most "textbook" use, but in Cloud Security, we mostly use **KMS (Key Management Service)** to handle this behind the scenes so we don't have to manage raw keys ourselves.

---

## Summary Matrix

| Use Case | Who has Public? | Who has Private? | Key Job |
| :--- | :--- | :--- | :--- |
| **SSH to EC2** | The EC2 Instance | You (The Human) | Identity Proof |
| **HTTPS Web** | Your Browser | The Web Server | Trust Setup |
| **Code Signing** | The Deployment Tool | The Developer | Integrity Check |
| **KMS / Data** | AWS Service | AWS Hardware (HSM) | Data Secrecy |