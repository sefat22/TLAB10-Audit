# TLAB10 — Cloud Compliance Audit & Remediation (AWS + Terraform)

## Project / Problem

This project simulates a real-world cloud security compliance audit for a fictional fintech company ("Titan Fintech"). The environment was intentionally provisioned with two common, high-risk misconfigurations:

- An AWS Security Group with SSH (port 22) open to the entire internet (`0.0.0.0/0`)
- An S3 bucket with public access enabled

The goal was to detect these violations using automated compliance tooling, document the findings, remediate the misconfigurations, and verify the fix — the same workflow a cloud security or DevSecOps engineer would run in a production environment.

## Approach

1. **Provisioned the vulnerable infrastructure** using Terraform (`main.tf`), including the insecure security group and public S3 bucket, to simulate a non-compliant environment.
2. **Deployed AWS Config** as the compliance monitoring layer, including an IAM role, configuration recorder, delivery channel, and logging bucket.
3. **Enabled AWS Config Rules** to continuously evaluate the environment against two compliance checks:
   - `INCOMING_SSH_DISABLED` — flags security groups with unrestricted SSH access
   - `S3_BUCKET_PUBLIC_READ_PROHIBITED` — flags publicly readable S3 buckets
4. **Captured pre-remediation evidence** showing both resources flagged as non-compliant.
5. **Remediated** the misconfigurations (restricting SSH access and locking down public S3 access).
6. **Captured post-remediation evidence** confirming both resources returned to a compliant state.
7. **Documented findings** in an executive-level audit report summarizing the risks, remediation steps, and outcome for a non-technical stakeholder audience.

## Tools & Technologies

- **Terraform** — infrastructure as code
- **AWS** — Security Groups, S3, IAM, AWS Config, Config Rules
- **AWS Config** — continuous compliance monitoring and rule evaluation

## Results / Outcomes

- Successfully identified two real, common cloud misconfigurations using automated compliance rules rather than manual inspection
- Remediated both findings and confirmed the change via AWS Config's compliance status
- Produced an executive audit report translating technical findings into business risk language — the kind of deliverable a compliance or security team would hand to leadership

## Project Evidence

- 📄 [`Executive_Audit_Report.pdf`](./Executive_Audit_Report.pdf) — full audit write-up
- 🖼️ [`TLAB-10 Pre-Remediation SS.png`](./TLAB-10%20Pre-Remediation%20SS.png) — AWS Config showing non-compliant resources
- 🖼️ [`TLAB - Post-Remediation SS.png`](./TLAB%20-%20Post-Remediation%20SS.png) — AWS Config showing resources returned to compliant status
- 🧱 [`main.tf`](./main.tf) — Terraform configuration for the audited environment

