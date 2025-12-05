---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/Jh7uJN5ZgBV4FyWQnmId/getting-started/installation-guide
---

# Installation Guide

This guide walks you through installing the **CyberShield SDKs and agents**, configuring credentials, and verifying your environment setup. Whether you’re deploying locally or in a CI/CD environment, follow these steps to ensure a secure and successful installation.

***

### Step 1: Prepare Your Environment

Before proceeding, confirm that your system meets the System Requirements and that you have:

* A valid **CyberShield API Key** and **API Secret**
* Administrative access to your system
* Outbound HTTPS access to `api.cybershield.io`
* Required SDK language runtime (Python, Node.js, or Java)

> 💡 **Tip:** Store credentials as environment variables to keep your configuration secure.

***

### Step 2: Install the CyberShield SDK

#### **Python SDK**

Install using `pip`:

<pre class="language-shellscript"><code class="lang-shellscript"><strong>bash
</strong>
pip install cybershield-sdk
</code></pre>

Initialize the SDK in your project:

```python
python

from cybershield import CyberShieldSDK

sdk = CyberShieldSDK(
    api_key="your_api_key",
    api_secret="your_api_secret"
)

sdk.connect()
print("✅ Connected to CyberShield API")
```

***

#### **Node.js SDK**

Install using `npm` or `yarn`:

```bash
bash

npm install cybershield-sdk
# or
yarn add cybershield-sdk
```

Initialize the SDK:

<pre class="language-javascript"><code class="lang-javascript"><strong>javascript
</strong>
<strong>const { CyberShieldSDK } = require("cybershield-sdk");
</strong>
const sdk = new CyberShieldSDK({
  apiKey: "your_api_key",
  apiSecret: "your_api_secret",
});

sdk.connect().then(() => {
  console.log("✅ Connected to CyberShield API");
});
</code></pre>

> **Security Tip:** Never hardcode credentials directly into your scripts. Use environment variables or secret management tools.

***

### 🖥 Step 3: Install the CyberShield Agent (Optional)

If you plan to use real-time network monitoring or endpoint protection features, install the local CyberShield Agent.

#### **Windows**

1. Download the latest agent package from the CyberShield Downloads page.
2. Run the installer as Administrator.
3. Follow on-screen prompts and enter your API credentials when prompted.
4.  Verify the agent service is running:

    <pre class="language-powershell"><code class="lang-powershell"><strong>powershell
    </strong>
    <strong>Get-Service CyberShieldAgent
    </strong></code></pre>

#### **Linux**

```bash
bash

curl -O https://cybershield.io/downloads/cybershield-agent-latest.tar.gz
tar -xzvf cybershield-agent-latest.tar.gz
cd cybershield-agent
sudo ./install.sh
```

Verify service status:

```bash
bash

sudo systemctl status cybershield-agent
```

> ⚠️ **Note:** If your system uses SELinux or AppArmor, ensure CyberShield processes are whitelisted.

***

### 🔍 Step 4: Verify the Installation

After installation, test your setup using the SDK’s built-in status command.

**Python:**

```bash
bash

python -m cybershield status
```

**Node.js:**

<pre class="language-bash"><code class="lang-bash"><strong>bash
</strong>
<strong>npx cybershield status
</strong></code></pre>

You should see:

```
yaml

✔ Connection: Active
✔ API Authentication: Successful
✔ Agent Status: Running
```

***

### ⚡ Step 5: Configure Environment Variables (Recommended)

Define these variables in your shell or CI/CD settings:

```bash
bash

export CYBERSHIELD_API_KEY="your_api_key"
export CYBERSHIELD_API_SECRET="your_api_secret"
export CYBERSHIELD_ENV="production"
```

To confirm:

```bash
bash

echo $CYBERSHIELD_API_KEY
```

> 💡 **Tip:** On Windows PowerShell, use `$env:CYBERSHIELD_API_KEY="your_api_key"` instead.

***

### Installation Complete

**Congratulations!**\
You’ve successfully installed and configured **CyberShield Security Suite** on your system.

> 💡 **Tip**_:_ Bookmark this page or save your configuration details for quick reference later.
