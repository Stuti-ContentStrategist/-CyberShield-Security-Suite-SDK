---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/Jh7uJN5ZgBV4FyWQnmId/developer-reference/integration-setup
---

# Integration Setup

Once installed, the CyberShield SDK allows your systems to communicate securely with CyberShield’s threat detection and reporting services. Integration ensures that security checks, scans, and alerts are automatically triggered as part of your application flow or DevOps process.

***

### Overview

This Integration Setup guides developers through connecting the CyberShield SDK to existing applications and services. It covers how to authenticate, verify connectivity, and embed the SDK into automation workflows such as CI/CD pipelines or monitoring systems.

By completing this setup, your systems can securely communicate with CyberShield’s security engine and report events in real time.

***

### Step 1 — Verify Prerequisites

Before integration, confirm you have:

| Requirement               | Description                                      |
| ------------------------- | ------------------------------------------------ |
| ✅ CyberShield Account     | Active developer or enterprise account           |
| ✅ API Credentials         | Your API key and secret (from Developer Console) |
| ✅ Supported Environment   | Python, Node.js, or Go                           |
| ✅ Outbound Network Access | HTTPS (port 443) allowed to CyberShield servers  |
| ✅ Permissions             | Developer or Admin role enabled                  |

> 💡 **Tip:** Use different credentials for development, staging, and production.
>
> 📘 **Note:** If you haven’t installed the SDK yet, see [Installation Guide](../getting-started/installation-guide.md).

***

### Step 2 — Initialize the SDK

Initialize the SDK using your credentials and environment configuration.\
You can use **environment variables**, **YAML**, or **JSON config files** depending on your setup.

**Example — Python**

```python
python

from cybershield import CyberShieldSDK

sdk = CyberShieldSDK(
    api_key="your_api_key",
    api_secret="your_api_secret",
    environment="production"
)
sdk.connect()
print("✅ CyberShield SDK connected successfully!")
```

> **Security Reminder:** Avoid hardcoding credentials — store them in environment variables or secret managers.

***

### Step 3 — Validate Your Integration

Test the connection to ensure the SDK is authenticated and ready to use.

```python
python

if sdk.health_check():
    print("✅ Connection successful! SDK is active and authorized.")
else:
    print("❌ Connection failed! Check credentials or network access.")
```

**Expected Output**

```
plain text

✅ Connection successful! SDK is active and authorized.
```

If this fails:

* Recheck API credentials
* Ensure outbound HTTPS isn’t blocked
* Confirm permissions in your CyberShield dashboard

***

### Step 4 — Embed into Your Workflow

You can integrate CyberShield SDK into:

| Use Case             | Description                                            |
| -------------------- | ------------------------------------------------------ |
| Application Security | Trigger vulnerability scans during deployment.         |
| CI/CD Pipelines      | Automate security checks in GitHub Actions or Jenkins. |
| Analytics            | Fetch threat reports and logs for dashboards.          |
| Compliance           | Include automated audit data in your security reports. |

**Example — GitHub Actions Workflow**

```yaml
name: CyberShield Security Scan
on: [push]
jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Run CyberShield Scan
        run: |
          python scripts/run_scan.py
```

***

Your integration is now complete — CyberShield SDK is securely connected and ready to power automated security workflows across your environment.
