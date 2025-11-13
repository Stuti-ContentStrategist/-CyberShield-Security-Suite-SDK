---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/Jh7uJN5ZgBV4FyWQnmId/developer-reference/authentication
---

# Authentication

This section explains how authentication works in the **CyberShield SDK**, including how to securely use API keys, generate access tokens, and enable Multi-Factor Authentication (MFA) for sensitive operations.

***

### 🧱 Overview

The CyberShield SDK uses a **two-layer authentication system** that ensures every request to CyberShield’s services is both verified and encrypted.

* **Layer 1:** API key and secret authenticate the SDK instance.
* **Layer 2:** Temporary access tokens (JWT) authorize specific operations during a session.

This layered design protects against credential misuse and supports enterprise-grade security requirements.

***

### 🔑 1. API Key-Based Authentication

When you initialize the SDK, your API key and secret authenticate your application to the CyberShield backend.

**Python Example**

```python
python

from cybershield import CyberShieldSDK

sdk = CyberShieldSDK(
    api_key="your_api_key",
    api_secret="your_api_secret",
    environment="production"
)
sdk.connect()
print("✅ SDK authenticated successfully!")
```

**Node.js Example**

```javascript
javascript

import { CyberShieldSDK } from "cybershield-sdk";

const sdk = new CyberShieldSDK({
  apiKey: process.env.CYBERSHIELD_API_KEY,
  apiSecret: process.env.CYBERSHIELD_API_SECRET,
  environment: "production"
});

await sdk.connect();
console.log("✅ SDK authenticated successfully!");
```

> 💡 **Tip:** Always store your credentials as **environment variables** — never in source code.

***

### 🧩 2. Token-Based Authentication (Session Tokens)

After the SDK authenticates your API key, it generates a **temporary access token** that expires after a set duration (default: 60 minutes).

Tokens eliminate the need to send your API secret with every request — improving both performance and security.

**Example — Retrieve and Refresh Token**

```python
python

token = sdk.get_access_token()
print(f"Active token: {token}")

# Refresh token when expired
sdk.refresh_token()
```

> ⚠️ **Important:**
>
> * Access tokens automatically expire — always refresh before making long-running API calls.
> * Avoid storing tokens in logs or cache files.

***

### 🧠 3. Multi-Factor Authentication (MFA)

CyberShield supports **biometric** and **token-based MFA** to protect high-privilege actions, such as configuration updates or API key rotation.

**Enabling MFA via SDK**

```python
python

sdk.enable_mfa(method="totp")
```

**Available Methods:**

| Method      | Description                                                |
| ----------- | ---------------------------------------------------------- |
| `totp`      | Time-based One-Time Password (using Authenticator app)     |
| `push`      | Mobile push notification approval                          |
| `biometric` | Fingerprint or facial recognition (supported systems only) |

> 🔒 **Best Practice:** Require MFA for all admin users or API clients managing sensitive configurations.

***

### ⚙️ 4. Handling Authentication Errors

If authentication fails, the SDK returns clear error codes to help diagnose the issue quickly.

| Error Code          | Meaning                   | Resolution                                        |
| ------------------- | ------------------------- | ------------------------------------------------- |
| `401_UNAUTHORIZED`  | Invalid API key or secret | Recheck your credentials in the Developer Console |
| `403_FORBIDDEN`     | MFA required or failed    | Verify MFA device or re-register it               |
| `408_TOKEN_EXPIRED` | Access token expired      | Use `sdk.refresh_token()` to renew                |
| `429_RATE_LIMITED`  | Too many requests         | Wait and retry after cooldown                     |



> 💡 **Tip:** Handle these gracefully in your integration scripts or pipelines using retry logic.

***

### 🧰 5. Rotating Credentials

To maintain security hygiene:

* Rotate API keys at least every **90 days**.
* Revoke unused or compromised keys immediately.
* Use the **CyberShield Developer Console** or Admin API for key management.

**Example**

```python
python

sdk.revoke_api_key("old_key_id")
sdk.generate_api_key(label="staging_env")
```

🔒 Authentication configured successfully — your SDK can now connect securely using verified API credentials.
