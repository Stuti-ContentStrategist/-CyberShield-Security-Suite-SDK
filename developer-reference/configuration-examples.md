---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/Jh7uJN5ZgBV4FyWQnmId/developer-reference/configuration-examples
---

# Configuration Examples

CyberShield SDK uses a modular configuration model. You can define parameters using **JSON**, **YAML**, or **environment variables**, depending on your workflow or CI/CD setup.

### 🧱 Overview

Configuration Examples demonstrate how to define and load CyberShield SDK settings for different environments. You’ll learn how to manage credentials, environment variables, and scanning parameters using YAML, JSON, or system variables.

These examples help you create consistent, secure configurations across development, staging, and production deployments.

***

Common configuration keys include:

| Key             | Description                                      | Example          |
| --------------- | ------------------------------------------------ | ---------------- |
| `api_key`       | Your CyberShield account API key                 | `"CS-6X29Q0..."` |
| `api_secret`    | Secret used for authentication                   | `"zKp8rA7..."`   |
| `environment`   | SDK environment (`dev`, `staging`, `production`) | `"production"`   |
| `region`        | Cloud region or deployment zone                  | `"us-east-1"`    |
| `scan_interval` | Frequency (in minutes) for automated scans       | `30`             |
| `enable_mfa`    | Enables multi-factor authentication              | `true`           |



***

### 🧩 Example 1 — YAML Configuration (Recommended)

Use a YAML file for human-readable configuration and easy version control.

`config/credentials.yaml`

```yaml
yaml

api_key: "your_api_key"
api_secret: "your_api_secret"
environment: "production"
region: "us-east-1"
enable_mfa: true
scan_interval: 15
log_level: "info"
```

Initialize SDK with a YAML file:

```python
python

from cybershield import CyberShieldSDK
import yaml

with open("config/credentials.yaml", "r") as f:
    config = yaml.safe_load(f)

sdk = CyberShieldSDK(**config)
sdk.connect()
```

> 💡 **Tip:** Exclude `credentials.yaml` from version control (`.gitignore`) to prevent key leaks.

***

### 🧩 Example 2 — Environment Variable Configuration

For CI/CD or container deployments, define configuration parameters as environment variables.

**Linux / macOS**

```bash
bash

export CYBERSHIELD_API_KEY="your_api_key"
export CYBERSHIELD_API_SECRET="your_api_secret"
export CYBERSHIELD_ENV="staging"
export CYBERSHIELD_SCAN_INTERVAL=20
```

**Windows (PowerShell)**

```powershell
powershell

$env:CYBERSHIELD_API_KEY="your_api_key"
$env:CYBERSHIELD_API_SECRET="your_api_secret"
$env:CYBERSHIELD_ENV="staging"
```

Load variables automatically:

```python
python

from cybershield import CyberShieldSDK
import os

sdk = CyberShieldSDK(
    api_key=os.getenv("CYBERSHIELD_API_KEY"),
    api_secret=os.getenv("CYBERSHIELD_API_SECRET"),
    environment=os.getenv("CYBERSHIELD_ENV", "production")
)
sdk.connect()
```

> 🧠 **Best practice:** Use this method in pipelines or Docker containers for security and automation.

***

### 🧩 Example 3 — JSON Configuration

You can also define configurations in JSON for compatibility with external systems.

`config/settings.json`

```json
json

{
  "api_key": "your_api_key",
  "api_secret": "your_api_secret",
  "environment": "dev",
  "region": "us-west-2",
  "enable_mfa": false
}
```

Load and initialize:

```javascript
javascript

const fs = require("fs");
const { CyberShieldSDK } = require("cybershield-sdk");

const config = JSON.parse(fs.readFileSync("./config/settings.json"));
const sdk = new CyberShieldSDK(config);

sdk.connect().then(() => console.log("✅ SDK connected"));
```

***

### 🔒 Security Considerations

* Never commit API keys or secrets to Git or shared repositories.
* Always use **environment variables** for CI/CD or production.
* Rotate keys periodically using your CyberShield admin dashboard.
* Store configurations in a **secrets manager** (AWS Secrets Manager, Vault, etc.) if available.

> ⚠️ **Warning:** Storing credentials in plain text can expose your system to credential theft or privilege escalation.

⚙️ Your SDK configuration is complete — your setup can now run optimized scans and secure data exchanges seamlessly.
