# Challenge 2: Android Cryptography Challenge – Intercepting and Decrypting Data

## Objective

Analyze and intercept encrypted HTTP communication between an Android application and its backend server. Identify cryptographic implementations, reverse them, and extract the hidden flag.

## Tools Used

- Burp Suite
- mitmproxy
- Wireshark
- APKTool
- JADX
- Python (for decryption scripting)

---

## Step-by-Step Process

### 1. Environment Setup

- Installed `Apk_task2` on a rooted emulator.
- Configured emulator Wi-Fi to route through Burp Suite proxy (via 10.0.2.2:8080).
- Installed Burp’s CA certificate on the device to enable HTTPS interception.

### 2. Intercepting HTTP Traffic

- Opened the app and observed encrypted traffic using Burp Suite.
- Captured POST request with JSON payload:
  ```json
  { "data": "U2FsdGVkX1+XzZ3Jm..." }
