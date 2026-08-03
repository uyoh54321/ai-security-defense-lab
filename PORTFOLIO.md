# AI Defense Lab — Portfolio

**Student:** Ebiloma Adejoh

**GitHub:** https://github.com/AibinuolaDamilola/ai-security-defense-lab/commit/a6575fe88f76c366a33c1fc917ad8018d7d9c139

**Hugging Face Space:** [Your HF Space URL]

**Completed:** 3/july/2026

---

Fill in each section as you complete a level. Link directly to your commit diff so a recruiter can see exactly what you changed.

---

## Level 1 — MedVitals AI · Cloud Infrastructure Security

**Problem:** A developer hardcoded live AWS credentials into the application's deployment configuration and committed them to a public GitHub repository. In addition, the IAM deployment role was configured with wildcard (Action: * and Resource: *) permissions, granting unrestricted administrative access. An attacker who discovered the exposed credentials could authenticate to the AWS environment, assume the privileged role, enumerate cloud resources, and access or modify sensitive patient data stored in Amazon S3.

**Method:** I investigated the deployment repository by reviewing the config.py and deploy-role-policy.json files to identify the security weaknesses. I then analyzed the AWS CloudTrail Event History to reconstruct the attack sequence and distinguish malicious activity from normal system events. To remediate the vulnerabilities, I replaced all hardcoded AWS credentials with environment variables using os.environ.get() and stored the secrets securely outside the source code. I also replaced the wildcard IAM policy with a least-privilege policy that grants only the permissions required by the application.

**Evidence:** https://github.com/AibinuolaDamilola/ai-security-defense-lab/commit/a6575fe88f76c366a33c1fc917ad8018d7d9c139

**Outcome:** The application no longer exposes AWS credentials in the source code, significantly reducing the risk of credential theft. The IAM role now follows the Principle of Least Privilege, limiting access to only the AWS resources required for normal operation. These improvements reduce the attack surface, better protect sensitive patient information, and strengthen the organization's overall cloud security posture. After implementing the fixes, Level 1 was successfully completed and Level 2 was unlocked.

**Skills:** CloudTrail Log Forensics · IAM Least Privilege · Secrets Management · Incident Timeline Reporting

**Others:**
- [Technical write-up link e.g. Medium blog post]
- [LinkedIn post link]
- [Any other documentation, video walkthrough, or public content]

---

## Level 2 — DataForge ML · AI Model Security

**Problem:**

**Method:**

**Evidence:** [Link to commit]

**Outcome:**

**Skills:** Model Supply Chain Verification · Pickle Exploit Detection · Safetensors · Automated Model Scanning

**Others:**
- [Technical write-up link]
- [LinkedIn post link]

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
