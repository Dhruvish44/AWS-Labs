# AWS Lab 13 – KMS Deep Dive: Encryption, Decryption & Envelope Encryption

## 📘 Overview
This lab demonstrates how to create a **Customer Managed KMS Key (CMK)**, encrypt/decrypt data using the AWS CLI, and implement envelope encryption.

**Goal →** Understand key usage and how AWS services use KMS for encryption.

---

## 🚀 Steps Performed
```text
1️⃣ Create a KMS CMK
aws kms create-key --description "Dhruvish Master Key" --key-usage ENCRYPT_DECRYPT

✅ Output includes Key ID and ARN.
```

```text
2️⃣ Create an Alias for Readability
aws kms create-alias --alias-name alias/dhruvish-key --target-key-id <KeyID>
```

```text
3️⃣ Encrypt Plaintext
echo "SensitiveData123" > secret.txt
aws kms encrypt \
--key-id alias/dhruvish-key \
--plaintext fileb://secret.txt \
--output text --query CiphertextBlob > encrypted.txt

✅ Data now encrypted with CMK.
```

```text
4️⃣ Decrypt Ciphertext
aws kms decrypt \
--ciphertext-blob fileb://encrypted.txt \
--output text --query Plaintext | base64 --decode

✅ Original data restored securely.
```

```text
5️⃣ Demonstrate Envelope Encryption
- Generate a data key under CMK:
aws kms generate-data-key \
--key-id alias/dhruvish-key \
--key-spec AES_256

✅ Returns plaintext and encrypted data key.
- Use plaintext key for local encryption (simulated).
- Discard plaintext; store encrypted key with data.
```

---

## 🧩 Verification
```bash
aws kms list-keys
aws kms describe-key --key-id alias/dhruvish-key
aws kms get-key-policy --key-id alias/dhruvish-key
```

---

## 🧠 Key Takeaways
- CMKs control encryption across AWS.  
- Envelope encryption improves speed & scalability.  
- Plaintext data keys should never be stored.  
- Always use **KMS CMKs** for compliance-grade protection.
