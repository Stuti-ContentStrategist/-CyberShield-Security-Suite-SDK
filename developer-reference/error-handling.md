---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/Jh7uJN5ZgBV4FyWQnmId/developer-reference/error-handling
---

# Error Handling

This section explains how to identify, handle, and log errors that occur while using the **CyberShield SDK**. Proper error handling ensures stability, improves resilience in CI/CD pipelines, and helps maintain secure operations.

***

### 🧱 Overview

CyberShield SDK provides structured error responses and exceptions across all supported languages.\
Each error includes:

* A **status code**
* A **message** explaining what went wrong
* A **recommendation** for resolution

By implementing consistent error handling, you can gracefully recover from temporary failures and capture diagnostics for auditing or debugging.

***

### 🧩 1. Common Error Types

| Error Type              | Description                            | Example Cause                | Recommended Action                  |
| ----------------------- | -------------------------------------- | ---------------------------- | ----------------------------------- |
| **AuthenticationError** | Invalid credentials or expired token   | Wrong API key or MFA failure | Recheck credentials / refresh token |
| **ConnectionError**     | Network connectivity issues            | Blocked HTTPS traffic        | Allow port 443 and retry            |
| **RateLimitError**      | Too many requests in short time        | High-frequency polling       | Implement exponential backoff       |
| **TimeoutError**        | Request took too long to respond       | Server overload or latency   | Increase timeout / retry            |
| **ValidationError**     | Incorrect request parameters           | Missing required field       | Correct API call syntax             |
| **InternalServerError** | Unexpected issue on CyberShield server | Temporary downtime           | Retry after a short delay           |

***

### 🧩 2. Handling Errors in Code

**Python Example**

<pre class="language-python"><code class="lang-python"><strong>python
</strong><strong>
</strong><strong>from cybershield import CyberShieldSDK, AuthenticationError, RateLimitError
</strong>
sdk = CyberShieldSDK(api_key="your_key", api_secret="your_secret")

try:
    sdk.connect()
    sdk.run_scan(target="internal_network")
except AuthenticationError:
    print("❌ Authentication failed. Please verify API credentials.")
except RateLimitError:
    print("⚠️ Rate limit exceeded. Retrying in 60 seconds...")
    time.sleep(60)
    sdk.run_scan(target="internal_network")
except Exception as e:
    print(f"🚨 Unexpected error: {e}")
</code></pre>

**Node.js Example**

<pre class="language-javascript"><code class="lang-javascript"><strong>javascript
</strong><strong>
</strong><strong>import { CyberShieldSDK, RateLimitError } from "cybershield-sdk";
</strong>
const sdk = new CyberShieldSDK({ apiKey: process.env.CS_KEY, apiSecret: process.env.CS_SECRET });

try {
  await sdk.connect();
  await sdk.runScan("staging-server");
} catch (error) {
  if (error instanceof RateLimitError) {
    console.warn("⚠️ Rate limit hit. Retrying in 30 seconds...");
    setTimeout(() => sdk.runScan("staging-server"), 30000);
  } else {
    console.error("❌ Integration error:", error.message);
  }
}
</code></pre>

> 💡 **Tip:** Always wrap API operations in `try/except` or `try/catch` blocks — this prevents your automation pipelines from breaking unexpectedly.

***

### 🧩 3. Error Logging

You can configure the SDK to log all warnings, errors, and failed requests.\
Logs help trace security incidents or connectivity failures.

**Python Example**

<pre class="language-python"><code class="lang-python"><strong>python
</strong><strong>
</strong><strong>sdk.configure_logging(level="error", logfile="cybershield_errors.log")
</strong></code></pre>

**Node.js Example**

```javascript
javascript

sdk.configureLogging({ level: "error", path: "./logs/cybershield.log" }
```

> 📘 **Recommendation:** Use structured logging (e.g., JSON format) to integrate with external log management systems such as Splunk, Datadog, or ELK Stack.

***

### 🧠 4. Retrying Failed Operations

Transient errors such as timeouts or rate limits can be recovered automatically using **retry logic**.

**Example (Python)**

```python
pyth

import time

for attempt in range(3):
    try:
        sdk.run_scan("production")
        break
    except TimeoutError:
        print(f"Attempt {attempt+1}/3 failed — retrying...")
        time.sleep(10)
```

> ⚙️ **Best Practice:**
>
> * Retry only for _transient_ issues (timeouts, rate limits, connection drops).
> * Do **not** retry on permanent errors (invalid credentials, permissions).
> * Use **exponential backoff** for cleaner network behavior.

***

### 🧩 5. Debug Mode

Enable debug logs for deeper inspection during development or troubleshooting:

```python
python

sdk.set_debug_mode(True)
```

This provides detailed traces for:

* API request payloads
* SDK initialization steps
* Response headers and timing

> ⚠️ **Security Note:** Debug mode may expose sensitive data (headers or tokens).\
> Use only in controlled, non-production environments.

***

### 🧰 6. Sample Error Response

Example of a structured error JSON returned by the CyberShield API:

```json
json

{
  "status": 403,
  "error": "FORBIDDEN",
  "message": "Multi-factor authentication required",
  "timestamp": "2025-11-06T08:42:17Z"
}
```

> 💡 **Tip:** Store these logs for auditing and include timestamps to track recurring failure patterns.

🧠 You’re now equipped to identify, log, and resolve SDK-related errors efficiently.
