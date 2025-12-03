---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/Jh7uJN5ZgBV4FyWQnmId/getting-started/system-requirements
---

# System Requirements

Before installing **CyberShield Security Suite**, ensure your environment meets the following prerequisites. Proper setup ensures optimal performance and compatibility across SDKs, agents, and the Security Dashboard.

***

### Supported Platforms

| Component          | Supported OS / Environment                            | Notes                                                            |
| ------------------ | ----------------------------------------------------- | ---------------------------------------------------------------- |
| **Dashboard**      | Web-based (Chrome, Edge, Firefox – latest 2 versions) | Best viewed at 1280×720 or higher                                |
| **SDKs**           | Python 3.9+, Node.js 16+, Java 11+                    | SDKs are language-specific — see Developer Reference → SDK Setup |
| **Agents**         | Windows 10+, Ubuntu 20.04+, CentOS 8+, Docker (v20+)  | Windows 7 support discontinued as of v5.0.0                      |
| **API Gateway**    | HTTPS endpoints (TLS 1.2 or later)                    | Legacy HTTP endpoints are deprecated                             |
| **Cloud Services** | AWS, Azure, GCP                                       | Requires API access and outbound internet connectivity           |

***

### Hardware Requirements

| Component | Minimum           | Recommended                   |
| --------- | ----------------- | ----------------------------- |
| CPU       | Dual-core 2.0 GHz | Quad-core 3.0 GHz+            |
| RAM       | 4 GB              | 8 GB+                         |
| Storage   | 5 GB free space   | 10 GB+ SSD preferred          |
| Network   | 10 Mbps           | 50 Mbps+ dedicated connection |

> 💡 **Tip:** For large-scale deployments (50+ agents or heavy scanning frequency), allocate dedicated VMs for the detection engine and API Gateway.

***

### Software Dependencies

| Requirement      | Version | Description                                        |
| ---------------- | ------- | -------------------------------------------------- |
| **Python**       | ≥ 3.9   | Required for Python SDK and CLI scripts            |
| **Node.js**      | ≥ 16    | Required for Node SDK integration                  |
| **Java Runtime** | ≥ 11    | Required for Java SDK                              |
| **Docker**       | ≥ 20    | Optional for containerized deployments             |
| **OpenSSL**      | ≥ 1.1   | Required for secure communication with the gateway |

> ⚠️ **Note:** Ensure all SDK environments have outbound internet access on ports **443** (HTTPS) and **8080** (API Gateway internal testing).

***

### Environment Variables

Before installation, confirm the following environment variables are available in your system or CI/CD environment:

```bash
CYBERSHIELD_API_KEY=your_api_key
CYBERSHIELD_API_SECRET=your_api_secret
CYBERSHIELD_ENV=production
CYBERSHIELD_LOG_LEVEL=info
```

For step-by-step initialization, see [Installation Guide.](installation-guide.md)

***

### Pre-installation Checklist

* [ ] Verify OS and SDK versions match supported configurations
* [ ] Ensure outbound HTTPS connectivity to `api.cybershield.io`
* [ ] Confirm valid license and API credentials
* [ ] Disable conflicting security software (if using local agents)
* [ ] Review Release Notes → v5.0.0 for compatibility changes

Once these checks are complete, your environment is fully prepared for CyberShield installation and SDK initialization.
