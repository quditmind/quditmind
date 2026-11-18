<p align="center">
  <img src="assets/quditmind-banner.svg" alt="QuditMind — open-source application security" width="100%">
</p>

<p align="center">
  <a href="https://github.com/quditmind/pathos/releases/latest"><img alt="Latest release" src="https://img.shields.io/github/v/release/quditmind/pathos?label=PATHOS&color=14B8A6"></a>
  <a href="https://github.com/quditmind/pathos/actions/workflows/ci.yml"><img alt="CI" src="https://github.com/quditmind/pathos/actions/workflows/ci.yml/badge.svg"></a>
  <a href="https://github.com/quditmind/pathos/blob/main/LICENSE"><img alt="License: Apache-2.0" src="https://img.shields.io/badge/license-Apache--2.0-4F46E5"></a>
  <a href="https://github.com/quditmind/pathos/security/policy"><img alt="Security policy" src="https://img.shields.io/badge/security-policy-0B1020"></a>
</p>

## About QuditMind

**QuditMind Private Limited** is an Indian software company that builds open-source application security tools. Our first product is **[PATHOS](https://github.com/quditmind/pathos)**, an Application Security Posture Management (ASPM) platform that you run on your own infrastructure.

| | |
|---|---|
| **Legal name** | QUDITMIND PRIVATE LIMITED |
| **Type** | Private company limited by shares, incorporated under the Companies Act, 2013 |
| **Incorporated** | 5 November 2026, Central Registration Centre, Ministry of Corporate Affairs, Government of India |
| **Corporate Identity Number (CIN)** | `U62020AP2026PTC129304` |
| **State of registration** | Andhra Pradesh, India |
| **Business activity** | Software and computer consultancy (NIC 62020) |

### Verify us yourself

You don't have to take our word for it:

1. **The company.** On the [Ministry of Corporate Affairs portal](https://www.mca.gov.in/), open *MCA Services → Master Data → View Company or LLP Master Data* and search for CIN `U62020AP2026PTC129304`. The official record shows the name, status, incorporation date and registered office.
2. **The code.** Everything is public under the Apache License 2.0: read it, build it, scan it.
3. **The releases.** Every release image is signed and can be checked before you run it (see below).

---

## PATHOS — Application Security Posture Management

PATHOS brings source-code scanning, findings management, vulnerability intelligence, SBOMs and posture analytics together in one self-hosted platform.

<p align="center">
  <img src="https://raw.githubusercontent.com/quditmind/pathos/v1.0.0/docs/user-guide/images/dashboard.png" alt="PATHOS security posture dashboard" width="49%">
  <img src="https://raw.githubusercontent.com/quditmind/pathos/v1.0.0/docs/user-guide/images/findings.png" alt="PATHOS findings list" width="49%">
</p>

- **Scanning:** Gitleaks, Opengrep, Trivy, Grype, OSV-Scanner, Checkov, zizmor and actionlint on repositories; container images, web applications and APIs (Nuclei), build artifacts and SBOMs as scan targets; your own tools as declarative plugins.
- **Repositories and assets:** GitHub, GitLab, Bitbucket Cloud and Azure DevOps, or local uploads; ownership, applications and business context.
- **Risk:** contextual 0–100 risk scores with EPSS, CISA KEV and OSV, reachability, attack paths, blast radius and posture by application, team or region.
- **Human Eye:** manual expert review with evidence, independent approval and full history.
- **AI, under your control:** AI-assisted triage and an AI Security Analyst with Anthropic, OpenAI, xAI or a **local model (Ollama)**. AI never decides on its own; people approve.
- **Governance:** security policies, SLAs, risk acceptance, compliance views (OWASP Top 10, ASVS, PCI DSS, ISO 27001, SOC 2), SSO with SAML or OIDC, MFA and an audit log.
- **Integrations:** REST API, webhooks (Slack, Microsoft Teams), Jira, ServiceNow, pull request checks and an MCP server.
- **Runs anywhere Docker runs**, including fully **air-gapped** installations.

### Install

The only requirement is Docker with the Compose plugin.

```bash
git clone --branch v1.0.0 https://github.com/quditmind/pathos.git && cd pathos
./deploy/scripts/install.sh      # generates .env with random secrets and prints the admin login
docker compose up -d --wait
```

Open `https://localhost` and sign in. To use the pre-built signed images instead of building locally, see [Installing a release](https://github.com/quditmind/pathos/blob/main/docs/OPERATIONS.md#installing-a-release-signed-images).

---

## Is it safe to use?

We build a security product, so we hold it to the standard we ask of others. Each point below can be checked independently.

| What | How you can check it |
|---|---|
| **Open source** | All code is public under [Apache-2.0](https://github.com/quditmind/pathos/blob/main/LICENSE). No closed components, no licence keys. |
| **Self-hosted, your data stays with you** | PATHOS runs on your servers. It does not call home to QuditMind, and every outbound connection is listed with its default in [docs/SECURITY.md](https://github.com/quditmind/pathos/blob/main/docs/SECURITY.md). Offline mode turns them all off. |
| **Signed releases** | Release images on `ghcr.io/quditmind` are signed with Sigstore cosign (keyless, tied to the release workflow) and carry an SBOM and SLSA provenance. |
| **Tested on every change** | CI runs unit, integration, browser and full-stack tests plus **gosec**, **govulncheck**, **Trivy** image scans and **OWASP ZAP** DAST (baseline and authenticated) against PATHOS itself. |
| **Supply chain** | Dependencies are pinned and updated by Dependabot; third-party GitHub Actions are pinned to commit SHAs. |
| **Least privilege** | Scoped role-based access control, CSRF protection, encrypted secrets at rest, isolated scan workers behind an egress proxy, and a complete audit log. |
| **Responsible disclosure** | Report vulnerabilities privately through [GitHub security advisories](https://github.com/quditmind/pathos/security/advisories/new); see the [security policy](https://github.com/quditmind/pathos/security/policy). |

Verify a release image before you deploy it:

```bash
cosign verify ghcr.io/quditmind/pathos:1.0.0 \
  --certificate-identity "https://github.com/quditmind/pathos/.github/workflows/release.yml@refs/tags/v1.0.0" \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

---

<p align="center">
  <img src="assets/quditmind-logo.svg" alt="QuditMind logo" width="72"><br>
  <sub>© 2026 QuditMind Private Limited · CIN U62020AP2026PTC129304 · PATHOS is licensed under Apache-2.0</sub>
</p>
