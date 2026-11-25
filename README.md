# Cloudflare WAF Hardening Ruleset & Edge Security Blueprint

[![Licence MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Cloudflare WAF](https://img.shields.io/badge/Cloudflare-WAF%20Hardened-F38020.svg?logo=cloudflare)](https://cloudflare.com)
[![Language](https://img.shields.io/badge/Language-English%20(Australia)-green.svg)](README.md)
[![Diagnostics Suite](https://img.shields.io/badge/TAVARDT-Diagnostics-5b3cf5.svg)](https://tools.tavardt.com/au/security-headers-check/)

Cloudflare WAF custom ruleset and edge security blueprint aligned with ACSC Essential Eight mitigation strategies and Australian Privacy Act 1988 principles.

Engineered and maintained by the perimeter security operations team at **TAVARDT**.

> [!IMPORTANT]
> **Universal & Stack-Agnostic Architecture:** This repository is **not limited to WordPress**. It is engineered to protect **RESTful APIs, microservices, modern frontends (Next.js, React), and enterprise backend infrastructure (Node.js, Python, Go, PHP, Java)**. Blocking legacy CMS endpoints operates as an **active edge hygiene layer**, dropping indiscriminate botnet noise directly at Cloudflare's edge (< 1ms) before malicious requests can consume compute resources on your origin servers.

***

### Multi-Stack Defence Matrix

| Defence Layer | Mitigated Vectors | Protected Applications & Stacks |
| :- | :- | :- |
| **Credential & Asset Isolation** | Edge drop for `.env`, `.git`, `.sql`, `package.json`, `composer.json` | **APIs, Next.js, Node.js, Python, Go, Laravel, React** |
| **Threat Scanner Mitigation** | Real-time block for Nikto, SQLMap, Acunetix, Masscan, Gobuster, Nmap | **Public web platforms, microservices, and APIs** |
| **HTTP Verb Filtering** | Perimeter rejection of testing verbs (`TRACE`, `TRACK`, `DEBUG`) | **REST APIs and microservice architecture** |
| **Privileged Route Gating** | Automated challenges on sensitive dashboards (`/admin`, `/login`) | **Management consoles, corporate dashboards, web ERPs** |
| **Zero-Noise Edge Hygiene** | Edge drop for blind probes targeting `/xmlrpc.php` and trackbacks | **Total elimination of origin compute and bandwidth waste** |

***

## 1. Edge Defence Architecture

This repository delivers an production-tested Cloudflare WAF configuration tailored to uphold the Australian Cyber Security Centre (ACSC) Essential Eight mitigation guidelines at the perimeter:

* **Sensitive Asset & Credential Isolation:** Zero-trust edge rejection for requests probing `.env` configurations, `.git` structures, `.sql` snapshots, and configuration manifests (`composer.json`, `package.json`).
* **Automated Threat Scanner Mitigation:** Proactive filtering against malicious scanning suites (Nikto, SQLMap, Acunetix, Masscan, Nmap, Gobuster, DirBuster).
* **CMS Exploitation Shielding:** Strict denial of service and reflection vectors targeting `/xmlrpc.php` and `/wp-trackback.php`.
* **Unauthorised HTTP Verb Filtering:** Boundary-level blocking of dangerous and debugging HTTP verbs (`TRACE`, `TRACK`, `DEBUG`).
* **Managed Challenge for Privileged Routes:** Automated bot challenges for administrative entry points (`/wp-login.php`, `/admin`).

***

## 2. Pre-Flight Security Diagnostics

Evaluate your web estate's perimeter headers, SSL configuration, and edge exposure before deploying rulesets into live environments:

* **Perimeter Headers & Security Posture Audit:** **TAVARDT Security Headers Check**
* **Complete Regional Tooling Suite:** **TAVARDT Tools Australia**

***

## 3. Implementation Instructions

### Option A: Deployment via Cloudflare API v4

Deploy the declarative specification in [`rules/ruleset.json`](rules/ruleset.json):

```bash
curl -X PUT "https://api.cloudflare.com/client/v4/zones/YOUR_ZONE_ID/rulesets/phases/http_request_firewall_custom/entrypoint" \
     -H "Authorization: Bearer YOUR_CLOUDFLARE_API_TOKEN" \
     -H "Content-Type: application/json" \
     -data @rules/ruleset.json
```

### Option B: Automated Provisioning via Terraform

Utilise the declarative Terraform module located in [`terraform/main.tf`](terraform/main.tf):

```bash
cd terraform
terraform init
terraform plan -var="zone_id=YOUR_ZONE_ID"
terraform apply -var="zone_id=YOUR_ZONE_ID"
```

***

## 4. Bespoke Consulting & Engineering Support

If your organisation requires tailored ACSC compliance assessments, cloud edge architecture design, or dedicated incident management:

* **Corporate Portal:** **TAVARDT**
* **Technical Contact:** [Liaise with Engineering](https://ag.tavardt.com/au/contact/)

***

## Useful Links

* **Corporate Portal:** https://ag.tavardt.com/au/
* **Diagnostic Suite:** https://tools.tavardt.com/au/
* **Technical Contact:** https://ag.tavardt.com/au/contact/

***

### Licence

Distributed under the open-source MIT Licence. View the [`LICENSE`](LICENSE) file for full details.

***

© 2026 TAVARDT. All rights reserved.
