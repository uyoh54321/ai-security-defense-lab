# AI Defense Lab — Portfolio

**Student:** Ebiloma Adejoh

**GitHub:** https://github.com/AibinuolaDamilola/ai-security-defense-lab/commit/a6575fe88f76c366a33c1fc917ad8018d7d9c139

**Hugging Face Space:** [Your HF Space URL]

**Completed:** 3/july/2026

---



---

## Level 1 — MedVitals AI · Cloud Infrastructure Security

**Problem:** A developer hardcoded live AWS credentials into the application's deployment configuration and committed them to a public GitHub repository. In addition, the IAM deployment role was configured with wildcard (Action: * and Resource: *) permissions, granting unrestricted administrative access. An attacker who discovered the exposed credentials could authenticate to the AWS environment, assume the privileged role, enumerate cloud resources, and access or modify sensitive patient data stored in Amazon S3.

**Method:** I investigated the deployment repository by reviewing the config.py and deploy-role-policy.json files to identify the security weaknesses. I then analyzed the AWS CloudTrail Event History to reconstruct the attack sequence and distinguish malicious activity from normal system events. To remediate the vulnerabilities, I replaced all hardcoded AWS credentials with environment variables using os.environ.get() and stored the secrets securely outside the source code. I also replaced the wildcard IAM policy with a least-privilege policy that grants only the permissions required by the application.

**Evidence:** https://github.com/AibinuolaDamilola/ai-security-defense-lab/commit/a6575fe88f76c366a33c1fc917ad8018d7d9c139

**Outcome:** The application no longer exposes AWS credentials in the source code, significantly reducing the risk of credential theft. The IAM role now follows the Principle of Least Privilege, limiting access to only the AWS resources required for normal operation. These improvements reduce the attack surface, better protect sensitive patient information, and strengthen the organization's overall cloud security posture. After implementing the fixes, Level 1 was successfully completed and Level 2 was unlocked.

**Skills:** CloudTrail Log Forensics · IAM Least Privilege · Secrets Management · Incident Timeline Reporting

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

**Problem:**

**Method:**

**Evidence:** [Link to commit]

**Outcome:**

**Skills:** AI API Hardening · Rate Limiting · Output Filtering · OWASP LLM Top 10 · Direct Prompt Injection Defence

**Others:**
- [Technical write-up link]
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
