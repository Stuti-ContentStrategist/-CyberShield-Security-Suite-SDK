---
metaLinks:
  alternates:
    - https://app.gitbook.com/s/Jh7uJN5ZgBV4FyWQnmId/troubleshooting/faqs
---

# FAQs

Find quick answers to common questions about setup, configuration, and usage. This section helps you troubleshoot frequent issues, clarify SDK behavior, and resolve errors without external assistance.

***

#### Q1: Why can’t I connect the SDK to my environment?

✅ Verify your API key and secret. Ensure your system clock is synchronized, as time drift can affect authentication.

***

#### Q2: I’m receiving too many alerts — how can I reduce noise?

✅ Adjust alert thresholds or disable low-priority event categories under **Policies → Manage Alerts**.

***

#### Q3: The dashboard isn’t updating in real time.

✅ Check your internet connection or refresh data using **Dashboard → Refresh Now**.

***

#### Q4: How can I reset my MFA or change authentication settings?

✅ Go to **Settings → Security → Multi-Factor Authentication** to reset tokens or update verification methods.

***

#### Q5: The installation failed with a “missing dependency” error.

✅ Re-run the installer as an administrator and ensure all prerequisites listed under **System Requirements** are installed.

***

#### Q6: Why am I seeing “Access Denied” for certain API endpoints?

✅ Confirm that your API token has the required permissions. Review role-based access settings under **Admin → Access Control**.

***

#### Q7: How do I integrate CyberShield with third-party tools like Slack or Jira?

✅ Navigate to **Integration Setup → Webhooks**, and follow the configuration steps for your preferred tool.

***

#### Q8: The scan results seem incomplete.

✅ Ensure all target subnets are included in your scan profile and that the agent is running with appropriate network privileges.

***

#### Q9: Can I export logs and reports?

✅ Yes. Go to **Dashboard → Reports → Export**, and choose between CSV, JSON, or PDF formats.

***

#### Q10: How can I contact support or report a bug?

✅ Visit **Support Channels** for contact options or open a ticket directly through your **CyberShield account dashboard**.

***

> 💡 **Tip**: If errors persist, check the `cybershield.log` file in your installation directory.

You’ve explored the most common questions users ask — and their solutions. For deeper insights, refer to our [Knowledge Base](https://app.gitbook.com/o/SxHNjM53o1ERQTNaTYLB/s/4DrWEAeXqgE1w4gMk9aV/).
