# EC2

## Key Pairs

- ED25519 is the modern default. Prefer over RSA unless legacy compatibility is needed.
- Private key is downloaded once at creation. AWS does not store it.
- Store in ~/.ssh/ with chmod 400.
- chmod 400 prevents accidental exposure but is not a substitute for full disk encryption.
- SSH command: ssh -i ~/.ssh/mykey.pem ec2-user@<public-ip>