# Cloudflare WAF Hardening Ruleset & Edge Security Blueprint | TAVARDT Australia

[![Licence MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Cloudflare WAF](https://img.shields.io/badge/Cloudflare-WAF%20Hardened-F38020.svg?logo=cloudflare)](https://cloudflare.com)
[![Language](https://img.shields.io/badge/Language-English%20(Australia)-green.svg)](README.md)
[![Diagnostics Suite](https://img.shields.io/badge/TAVARDT-Diagnostics-5b3cf5.svg)](https://tools.tavardt.com/au/security-headers-check/)

Cloudflare WAF custom ruleset and edge security blueprint aligned with ACSC Essential Eight mitigation strategies and Australian Privacy Act 1988 principles.

Engineered and maintained by the perimeter security operations team at **[TAVARDT Australia](https://ag.tavardt.com/au/cybersecurity/)**.

---

## 1. Edge Defence Architecture

This repository delivers an production-tested Cloudflare WAF configuration tailored to uphold the Australian Cyber Security Centre (ACSC) Essential Eight mitigation guidelines at the perimeter:

* **Sensitive Asset & Credential Isolation:** Zero-trust edge rejection for requests probing `.env` configurations, `.git` structures, `.sql` snapshots, and configuration manifests (`composer.json`, `package.json`).
* **Automated Threat Scanner Mitigation:** Proactive filtering against malicious scanning suites (Nikto, SQLMap, Acunetix, Masscan, Nmap, Gobuster, DirBuster).
* **CMS Exploitation Shielding:** Strict denial of service and reflection vectors targeting `/xmlrpc.php` and `/wp-trackback.php`.
* **Unauthorised HTTP Verb Filtering:** Boundary-level blocking of dangerous and debugging HTTP verbs (`TRACE`, `TRACK`, `DEBUG`).
* **Managed Challenge for Privileged Routes:** Automated bot challenges for administrative entry points (`/wp-login.php`, `/admin`).

---

## 2. Pre-Flight Security Diagnostics

Evaluate your web estate's perimeter headers, SSL configuration, and edge exposure before deploying rulesets into live environments:

* **Perimeter Headers & Security Posture Audit:** [TAVARDT Australia Security Headers Check](https://tools.tavardt.com/au/security-headers-check/)
* **Complete Regional Tooling Suite:** [TAVARDT Tools Australia](https://tools.tavardt.com/au/)

---

## 3. Implementation Instructions

### Option A: Deployment via Cloudflare API v4

Deploy the declarative specification in [`rules/ruleset.json`](rules/ruleset.json):

```bash
curl -X PUT "https://api.cloudflare.com/client/v4/zones/YOUR_ZONE_ID/rulesets/phases/http_request_firewall_custom/entrypoint" \
     -H "Authorization: Bearer YOUR_CLOUDFLARE_API_TOKEN" \
     -H "Content-Type: application/json" \
     --data @rules/ruleset.json
```

### Option B: Automated Provisioning via Terraform

Utilise the declarative Terraform module located in [`terraform/main.tf`](terraform/main.tf):

```bash
cd terraform
terraform init
terraform plan -var="zone_id=YOUR_ZONE_ID"
terraform apply -var="zone_id=YOUR_ZONE_ID"
```

---

## 4. Bespoke Consulting & Engineering Support

If your organisation requires tailored ACSC compliance assessments, cloud edge architecture design, or dedicated incident management:

* **Corporate Portal:** [TAVARDT Australia](https://ag.tavardt.com/au/cybersecurity/)
* **Technical Contact:** [Liaise with Engineering](https://ag.tavardt.com/au/contact/)

---

## Licence

Distributed under the open-source MIT Licence. View the [`LICENSE`](LICENSE) file for full details.  
Copyright (c) 2026 TAVARDT Australia.
