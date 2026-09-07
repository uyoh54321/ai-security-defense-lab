# AI Defense Lab — Portfolio

**Student:** Ebiloma Adejoh

**GitHub:** https://github.com/AibinuolaDamilola/ai-security-defense-lab/commit/a6575fe88f76c366a33c1fc917ad8018d7d9c139

**Hugging Face Space:** [Your HF Space URL]

**Completed:** 3/july/2026

---



---

## Level 1 — MedVitals AI · Cloud Infrastructure Security

**Scenario/Investigation:** MedVitals AI is a simulated HealthTech application requiring a cloud infrastructure security assessment.

I investigated the application's deployment configuration and AWS environment to identify exposed credentials, excessive IAM permissions, and potential attack paths to sensitive cloud resources.

I reviewed the deployment repository, including 'config.py' and  'deploy-role-policy.json ', and analyzed AWS CloudTrail Event History to reconstruct the potential attack sequence and distinguish malicious activity from normal system events.

**Problem/Vulnirability:** I identified two significant cloud security vulnerabilities:

**1. Exposed AWS Credentials**

Live AWS credentials were hardcoded into the application's deployment configuration and committed to a public GitHub repository.

An attacker who discovered the exposed credentials could potentially authenticate to the AWS environment, assume the privileged deployment role, enumerate cloud resources, and access or modify sensitive patient data stored in Amazon S3.

**2. Excessive IAM Permissions**

The deployment IAM role was configured with unrestricted wildcard permissions:

Action: *
Resource: *

This violated the Principle of Least Privilege by granting the role access beyond what the application required.

The combination of exposed credentials and excessive IAM permissions significantly increased the potential impact of a credential compromise.

**Evidence:** 
The investigation was supported by:

* `config.py` — deployment configuration containing the exposed AWS credentials.
* `deploy-role-policy.json` — IAM policy containing wildcard permissions.
* AWS CloudTrail Event History — used to reconstruct the potential attack sequence and distinguish malicious activity from normal system events.
* GitHub remediation commit documenting the security changes.

### Remediation Commit
https://github.com/AibinuolaDamilola/ai-security-defense-lab/commit/a6575fe88f76c366a33c1fc917ad8018d7d9c139

## Remediation

I removed the hardcoded AWS credentials from the application's source code and replaced them with environment-based configuration using:

```python
os.environ.get()
```

This ensures that sensitive credentials are stored outside the source code rather than being embedded directly in the application.

I also replaced the wildcard IAM policy with a **least-privilege IAM policy**, granting only the permissions required by the application.

These changes address both major findings by reducing the risk of credential exposure and limiting the potential impact of a compromised AWS identity.


## Commit

[Level 1 — Cloud Security Remediation Commit](https://github.com/AibinuolaDamilola/ai-security-defense-lab/commit/a6575fe88f76c366a33c1fc917ad8018d7d9c139)

## Outcome

After remediation:

* AWS credentials are no longer exposed in the application's source code.
* The deployment IAM role follows the Principle of Least Privilege.
* Access is restricted to the AWS resources and permissions required for normal application operation.
* The overall cloud attack surface is reduced.
* Sensitive patient information receives stronger protection.

**Level Status: Completed**

Level 1 was successfully completed and Level 2 was unlocked.

## Skills Demonstrated

* **CloudTrail Log Forensics**
* **IAM Least Privilege**
* **Secrets Management**
* **Incident Timeline Reporting**

## Supporting Artifacts

* Deployment configuration analysis
* IAM policy analysis
* AWS CloudTrail Event History analysis
* GitHub remediation commit




**Others:**
- https://medium.com/@uyoh54321/investigating-a-cloud-security-incident-at-medvitals-ai-level-1-23618ef6824a
-  https://www.linkedin.com/posts/adejoh_cybersecurity-cloudsecurity-aws-activity-7490134613768536064-9g76?                                  utm_source=share&utm_medium=member_ios&rcm=ACoAAC006sYBsguhtWGOFfe1PWJIvpnCPGq7ggk
-  
- 

---

## Level 2 — DataForge ML · AI Model Security

**Problem:** The application was downloading a machine-learning model from an external Hugging Face repository and loading it using Python's pickle.load.

The security concern was that a Pickle file can contain executable Python objects. If the model had been modified or maliciously packaged, loading it could potentially allow code execution inside the application environment.

**Method:** I approached it as a practical security investigation:

1)Inspected the model-loading code to understand how the application obtained and loaded the model.
2)Identified the external model source on Hugging Face.
3)Recognized the security risk of Python Pickle deserialization.
4)Used PickleScan to scan the model artifact.
5)Analyzed the scan results rather than assuming the model was safe.
6)Mapped the findings to OWASP LLM and MITRE ATLAS as required by the assessment.
7)Documented the risk and remediation in an eight-field Model Threat Assessment.
8)Recommended controls such as model provenance verification, artifact scanning, safer serialization, model isolation, and integrity        checking.

**Evidence:** https://github.com/uyoh54321/ai-security-defense-lab/commit/4f8d58fb579f3a09b77e62d066c7affced56530c

**Outcome:** I was able to demonstrate that the model artifact should not automatically be trusted.

The scan provided concrete evidence of a security concern: one dangerous global was detected.

i then converted that technical finding into a business-level risk assessment explaining:

What happened → why it matters → potential impact → what should be done about it.

That's an important outcome because you didn't just run a security tool—you interpreted the result and translated it into a security decision.

**Skills:** Model Supply Chain Verification · Pickle Exploit Detection · Safetensors · Automated Model Scanning

**Others:**
- https://github.com/uyoh54321/hernetiq-fellowship-portfolio/blob/main/week%20-6/Model%20Threat%20Assessment.md
- https://www.linkedin.com/posts/adejoh_aisecurity-cybersecurity-ai-activity-7495982538427899904-oDdm?
  utm_source=share&utm_medium=member_ios&rcm=ACoAAC006sYBsguhtWGOFfe1PWJIvpnCPGq7ggk

---

## Level 3 — CartBot AI · Application & API Security

**Problem:**CartBot AI’s customer-facing API trusted a client-supplied `customer_id` header with no cryptographic verification.

**Method:** Audited `api_config.py` and identified `TRUST_CUSTOMER_ID_HEADER = True`, `REQUIRE_JWT_VALIDATION = False`, and `RATE_LIMIT_ENABLED = False`. Queried the CartBot AI assistant to trigger the indirect prompt injection, demonstrated BOLA by accessing another customer’s orders, ran the Bulk Harvest simulation, and used Semgrep to identify the vulnerable patterns.

**Evidence:** https://github.com/uyoh54321/ai-security-defense-lab/commit/0325456214cc16b869e1598573ac6e849c4454b1

**Outcome:** The API can no longer be BOLA’d via header spoofing — JWT validation verifies the requester and requested customer ID, rate limiting is enabled, and the system prompt restricts customer-data retrieval while treating product content as untrusted data.

**Skills:** AI API Hardening · Rate Limiting · Output Filtering · OWASP LLM Top 10 · Direct Prompt Injection Defence, MITRE ATLAS AML.T0054 (LLM Data Exfiltration) · JWT authentication · Rate limiting / Denial of Wallet mitigation · Semgrep static analysis · Defence-in-depth architecture

**Others:**
- https://github.com/uyoh54321/hernetiq-fellowship-portfolio/blob/main/week%208/API%20security%20threat%20model.md
- [LinkedIn post link]

---

## Level 4 — PayGuard · Data Security in AI

**Problem:**

**Method:**

**Evidence:** [Link to commit]

**Outcome:**

**Skills:** STRIDE Threat Modeling · RAG Pipeline Security · Multi-Tenant Data Isolation · Indirect Prompt Injection Defence

**Others:**
- [Technical write-up link]
- [LinkedIn post link]

---

## Level 5 — LegalBot Municipal · Agentic AI Security

**Problem:**

**Method:**

**Evidence:** [Link to commit]

**Outcome:**

**Skills:** Excessive Agency Mitigation · Llama Guard Integration · Pydantic Schema Enforcement · Autonomous Agent Containment

**Others:**
- [Technical write-up link]
- [LinkedIn post link]
