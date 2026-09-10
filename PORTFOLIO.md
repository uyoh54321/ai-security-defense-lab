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

## Scenario / Investigation

DataForge ML is a simulated machine-learning application that downloads a machine-learning model from an external Hugging Face repository.

I investigated the application's model-loading process to determine whether the externally sourced model artifact could introduce a security risk when loaded into the application environment.

The investigation focused on the use of Python's `pickle.load` for model deserialization.

## Problem / Vulnerability

The application downloaded an ML model from an external Hugging Face repository and loaded it using:

```python
pickle.load()
```

The security concern was that Python Pickle files can contain executable Python objects. If the model artifact had been modified or maliciously packaged, loading it could potentially allow code execution inside the application environment.

The key security issue was the implicit trust placed in an externally sourced model artifact during deserialization.

**Evidence:** https://github.com/uyoh54321/ai-security-defense-lab/commit/4f8d58fb579f3a09b77e62d066c7affced56530c

## Evidence

I conducted the following investigation:

1. Inspected the model-loading code to understand how the application obtained and loaded the model.
2. Identified the external model source on Hugging Face.
3. Analyzed the security risk associated with Python Pickle deserialization.
4. Used **PickleScan** to scan the model artifact.
5. Analyzed the scan results rather than assuming the model was safe.
6. Mapped the finding to **OWASP LLM** and **MITRE ATLAS**.
7. Documented the risk using an eight-field **Model Threat Assessment**.

The PickleScan scan detected **one dangerous global**, providing concrete evidence that the model artifact required further security assessment.

### Evidence Commit

[View GitHub Commit](https://github.com/uyoh54321/ai-security-defense-lab/commit/4f8d58fb579f3a09b77e62d066c7affced56530c)

## Remediation

Based on the investigation, I identified controls to reduce the risk associated with externally sourced model artifacts.

Recommended controls included:

* **Model provenance verification** — verify where the model originated and whether the source is trusted.
* **Automated model scanning** — scan model artifacts before they are loaded or deployed.
* **Safer serialization** — use safer model serialization formats such as **Safetensors** where supported.
* **Model isolation** — isolate model loading and execution from sensitive application resources.
* **Integrity checking** — verify model artifacts have not been modified before use.

I also converted the technical finding into a business-level risk assessment covering:

**What happened → Why it matters → Potential impact → What should be done**

## Commit

[Level 2 — Model Security Assessment Commit](https://github.com/uyoh54321/ai-security-defense-lab/commit/4f8d58fb579f3a09b77e62d066c7affced56530c)

## Outcome

The investigation demonstrated that an externally sourced machine-learning model artifact should **not automatically be trusted**.

PickleScan provided concrete evidence of a security concern by detecting one dangerous global in the model artifact.

I then translated the technical finding into a security decision by documenting the risk, potential impact, and recommended controls.

This investigation strengthened my ability to assess **AI model supply-chain risk**, interpret model-scanning results, and communicate technical security findings at both technical and business levels.

**Level Status: Completed**

## Skills Demonstrated

* **Model Supply Chain Verification**
* **Pickle Exploit Detection**
* **Safetensors**
* **Automated Model Scanning**

## Supporting Artifacts

* PickleScan model scan
* Eight-field Model Threat Assessment
* OWASP LLM mapping
* MITRE ATLAS mapping
* GitHub evidence / assessment commit

**Others:**
- https://github.com/uyoh54321/hernetiq-fellowship-portfolio/blob/main/week%20-6/Model%20Threat%20Assessment.md
- https://www.linkedin.com/posts/adejoh_aisecurity-cybersecurity-ai-activity-7495982538427899904-oDdm?
  utm_source=share&utm_medium=member_ios&rcm=ACoAAC006sYBsguhtWGOFfe1PWJIvpnCPGq7ggk

---

## Level 3 — CartBot AI · Application & API Security
## Scenario / Investigation

CartBot AI is a simulated AI-powered e-commerce application requiring an application and API security assessment.

I investigated the application's authentication, authorization, prompt-injection, data-exfiltration, and rate-limiting controls.

I reviewed `api_config.py`, interacted with the CartBot AI assistant, tested for indirect prompt injection, demonstrated Broken Object Level Authorization (BOLA), ran the Bulk Harvest simulation, and used Semgrep to identify vulnerable patterns.

## Problem / Vulnerability

The API trusted a client-supplied `customer_id` header without cryptographic verification.

The application configuration contained:

```text
TRUST_CUSTOMER_ID_HEADER = True
REQUIRE_JWT_VALIDATION = False
RATE_LIMIT_ENABLED = False
```

This created multiple security weaknesses.

### 1. Broken Object Level Authorization (BOLA)

Because the API trusted the client-supplied `customer_id`, I was able to demonstrate unauthorized access to another customer's orders by manipulating the customer identifier.

### 2. Authentication Weakness

JWT validation was disabled, meaning the API did not properly validate the identity associated with the request before processing customer-data requests.

### 3. Rate-Limiting Weakness

Rate limiting was disabled, increasing the risk of automated requests, bulk harvesting, and Denial-of-Wallet scenarios.

### 4. Indirect Prompt Injection

I also tested the CartBot AI assistant for indirect prompt injection involving untrusted product content and customer-data retrieval.

## Evidence

The investigation included:

* Review of `api_config.py`.
* Testing of the CartBot AI assistant.
* Indirect prompt-injection testing.
* BOLA demonstration by manipulating the customer ID.
* Bulk Harvest simulation.
* Semgrep static analysis to identify vulnerable patterns.
### Remediation Commit

[View GitHub Commit](https://github.com/uyoh54321/ai-security-defense-lab/commit/0325456214cc16b869e1598573ac6e849c4454b1)

## Remediation

I implemented multiple security controls to address the identified weaknesses.

### Authentication and Authorization

JWT validation was enabled to verify the requester.

Authorization controls were added to verify that the authenticated requester is permitted to access the requested customer ID.

The client-supplied customer ID was no longer treated as a trusted security boundary.

### Rate Limiting

Rate limiting was enabled to reduce automated abuse, bulk harvesting, and Denial-of-Wallet risk.

### Prompt Injection Defense

The system prompt was strengthened to restrict customer-data retrieval.

Product content was treated as **untrusted data** rather than trusted instructions.

### Defense in Depth

Output filtering and Semgrep static analysis were used as additional defensive layers.

The remediation follows a **defense-in-depth** approach rather than relying on a single security control.

## Commit

[Level 3 — Application & API Security Remediation Commit](https://github.com/uyoh54321/ai-security-defense-lab/commit/0325456214cc16b869e1598573ac6e849c4454b1)

## Outcome

The API can no longer be BOLA'd through the previously demonstrated header-spoofing path.

JWT validation now verifies the requester, while authorization controls verify access to the requested customer data.

Rate limiting reduces the ability to perform automated bulk requests.

The system-prompt controls establish stronger boundaries around customer-data retrieval while treating product content as untrusted input.

These controls reduce exposure to:

* Unauthorized customer-data access
* Automated data harvesting
* Prompt-injection-driven data exposure
* Denial-of-Wallet scenarios

**Level Status: Completed**

## Skills Demonstrated

* **AI API Hardening**
* **JWT Authentication**
* **Object-Level Authorization**
* **Rate Limiting**
* **Denial-of-Wallet Mitigation**
* **Output Filtering**
* **OWASP LLM Top 10**
* **Prompt Injection Defense**
* **MITRE ATLAS AML.T0054 — LLM Data Exfiltration**
* **Semgrep Static Analysis**
* **Defense-in-Depth Architecture**

## Supporting Artifacts

* API configuration audit
* BOLA demonstration
* Bulk Harvest simulation
* Prompt-injection testing
* Semgrep static-analysis results
* GitHub remediation commit

**Others:**
- https://github.com/uyoh54321/hernetiq-fellowship-portfolio/blob/main/week%208/API%20security%20threat%20model.md
- https://www.linkedin.com/posts/adejoh_aisecurity-cybersecurity-apisecurity-activity-7501320215545270272-G3Nn?utm_source=share&utm_medium=member_ios&rcm=ACoAAC006sYBsguhtWGOFfe1PWJIvpnCPGq7ggk 

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
