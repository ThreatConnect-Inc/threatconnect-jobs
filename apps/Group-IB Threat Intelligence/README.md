# Group-IB Threat Intelligence

User Documentation:
https://github.com/ThreatConnect-Inc/threatconnect-jobs/blob/master/apps/Group-IB%20Threat%20Intelligence/GIB_TI_ThreatConnect_User_Guide.pdf

# Release Notes

## 1.0.0 (YYYY-MM-DD)

- Initial Release

## 1.0.1 (2021-02-21)

- Minor bugs fixes

## 1.0.2 (2021-03-26)

- Phishing IPs and Domains deprecation.

## 1.0.3 (2021-08-02)

- Malware CNC IPs attributes added(First Seen, Last Seen) + additional Malware name tags

## 1.0.4 (2023-03-25)

- Extra fields added to reports for the next collections: Threat, Threat Actor

## 1.2.0 (2024-02-22)

- Refactored connection logic
- Data ingestion logic update
- New collections added:
  - attacks/phishing_group
  - compromised/access
  - compromised/account_group
  - compromised/bank_card
  - compromised/masked_card
  - compromised/messenger
  - hi/open_threats
  - ioc/common
  - osi/git_repository
  - suspicious_ip/vpn
  - suspicious_ip/scanner
- Deprecated collections removed:
  - compromised/account
  - attacks/phishing
  - bp/phishing
  - bp/phishing_kit
  - malware/targeted_malware
  - osi/code_repository
- About 50 fields where added to old collections' objects

## 1.3.0 (2025-12-18)

### New Features

- **Replaced Compromised Data :: Mules with Compromised Data :: SPD (Suspicious Payment Details)**: The `compromised_mule` collection has been replaced with `compromised_spd` to better reflect the nature of the data.
- **Enhanced Compromised Data :: Accounts filtering**: Added three new filter flags for the `compromised_account_group` collection:
  - **Is in combolist?** (`compromised_account_group_combo`): Filter accounts detected as a part of combolists
  - **Is a unique record?** (`compromised_account_group_unique`): Filter for accounts from unique detection records
  - **Filter for probable corporate access?** (`compromised_account_group_corp`): Filter accounts with probable corporate access indicators

### Improvements

- **Batch submission logic**: Fixed and improved batch submission logic to enhance data processing efficiency and reliability
- **Code refactoring**: Major code refactoring and improvements for better maintainability and code quality
- **Error handling**: Enhanced error handling and logging throughout the application for better debugging and monitoring
- **Documentation**:
  - Improved overall documentation and user guidance
- **Attributes**: Updated attribute definitions and mappings to support new data types and improve data accuracy

## 1.4.0 (2026-07-31)

### New collections

- **Compromised Data :: Breached DB** (`compromised/breacheddb`) — credentials/records from breached databases.
- **Darkweb :: Forums** (`darkweb/forums`) — dark-web forum posts.
- **IOC :: Primary** (`ioc/primary`) — primary IOC feed with per-indicator risk scores and evaluation.

### Richer context on ingested objects

- **Evaluation** attached across feeds: Admiralty Code, Credibility (Attribution Confidence), Reliability, Severity, and TLP (Security Label).
- **Threat Actor** and **Malware Family** context attached to the relevant groups and indicators.
- **Group-IB portal deep-links** added to groups (Additional Analysis and Context), toggled by _Attach portal links_.
- **Compromised Data :: Git Leaks** now includes evaluation, source, repository/contributor context, and pivot tags such as `Credentials Found` and `Private Key Found` (previously a link only).
- **OSI :: Vulnerability** now includes CVSS score, EPSS, exploit availability (Has Exploit), and CVE references.
- **Suspicious IP** feeds now include hosting provider, country, city, and ASN.
- Additional per-collection fields (e.g. DDoS target details, phishing-kit source/login, malware-config summary, signature/YARA source and dates).

### Filtering

- **Hunting Rules** — a 3-state control per supporting collection (_API default_ / _Apply_ / _Do not apply_); see the **Hunting rules** section below.
- **Optional filters** — Suspicious Payment Details type, IOC network/file scope, account combolist / probable-corporate-access, breached-DB has-password, and malware description; see the **Optional filters** section below.

### Under the hood

- Updated to the maintained **ciaops 3.0.0** library.

# ThreatConnect Group-IB TI Integration Setup Guide

This document outlines the steps required to set up and configure the Group-IB Threat Intelligence integration with the ThreatConnect Platform.

---

## Before You Begin

Ensure the following prerequisites are met before starting the installation:

- **Supported Platform:** You must be running a **supported version of the ThreatConnect Platform**.
- **Application Pre-Check:** Verify that the **TC Group-IB TI application has been installed without errors** (if a previous attempt was made).
- **Credentials:** Make sure you have **valid Group-IB and ThreatConnect API credentials**.

---

## Step 1: Download the Integration

1.  Navigate to the **Group-IB TI Help Center**.
2.  Go to: **Integrations** $\rightarrow$ **Custom and native integrations** $\rightarrow$ **ThreatConnect**.
3.  **Download the latest version of the integration archive.**

---

## Step 2: Create a ThreatConnect API User

You will need a specific API user for this integration.

1.  **Login to the ThreatConnect web interface as an administrator.**
2.  Click the **Gear icon** (top right) $\rightarrow$ **Org Settings**.
3.  In the **Membership** tab, click **Create API User**.
4.  **Save the API token** - this is crucial for the subsequent configuration.

---

## Step 3: Install the Application

1.  Go to **Gear** $\rightarrow$ **Org Settings** $\rightarrow$ **Apps**.
2.  Click **Install App**.
3.  **Extract the downloaded ZIP archive** to get the **`.tcx`** file.
4.  **Upload the `.tcx` file**.
5.  Click **Install**.

---

## Step 4: Upload Attribute Types

New attribute types are required to store Group-IB's unique data points.

1.  **Extract the `.tcx` file** (if not already done in Step 3).
2.  Locate the **`attributes.json`** file inside the app folder.
3.  In ThreatConnect, go to **Gear** $\rightarrow$ **Org Settings** $\rightarrow$ **Attribute Types**.
4.  Click **Upload**, select **`attributes.json`**, and click **Save**.
5.  **New attributes will now appear in the list.**

---

## Step 5: Verify Installation

Ensure your credentials and the app installation are correct.

1.  **Verify** you have the correct **Group-IB TI username and API token**. Consult the **Group-IB Starting Guide** for more information on these.
2.  Once installation is complete, you should see the **“Group-IB Threat Intelligence (vx.x.x)” app** listed at:
    **Gear** $\rightarrow$ **Org Settings** $\rightarrow$ **Apps tab** $\rightarrow$ **Add Job menu** $\rightarrow$ **Run Program dropdown**.

---

## Step 6: Create a Job

1.  **Follow the instructions in the Configuration section in the extended documentation guide** to create a new job for the app and begin data synchronization.

---

# Reference

## Supported collections (33)

- **apt** — `apt/threat`, `apt/threat_actor`
- **attacks** — `attacks/ddos`, `attacks/deface`, `attacks/phishing_group`, `attacks/phishing_kit`
- **compromised** — `compromised/access`, `compromised/account_group`,
  `compromised/bank_card_group`, `compromised/breacheddb`, `compromised/discord`,
  `compromised/masked_card`, `compromised/messenger`, `compromised/spd`
- **darkweb** — `darkweb/forums`
- **hi** — `hi/open_threats`, `hi/threat`, `hi/threat_actor`
- **ioc** — `ioc/common`, `ioc/primary`
- **malware** — `malware/cnc`, `malware/config`, `malware/malware`, `malware/signature`, `malware/yara`
- **osi** — `osi/git_repository`, `osi/public_leak`, `osi/vulnerability`
- **suspicious_ip** — `suspicious_ip/open_proxy`, `suspicious_ip/scanner`,
  `suspicious_ip/socks_proxy`, `suspicious_ip/tor_node`, `suspicious_ip/vpn`

## Hunting rules (`apply_hunting_rules`)

`apply_hunting_rules` filters a feed to records matching your org's hunting rules
(a **subset** of the full feed). Each supported collection has a 3-state
**Hunting Rules** input:

- **`API default`** (default) — the integration sends no parameter and the GIB
  API applies its own default.
- **`Apply (1)`** — send `apply_hunting_rules=1` (filter to hunting-rule matches).
- **`Do not apply (0)`** — send `apply_hunting_rules=0` (ingest the full feed).

> ⚠️ The GIB API enables hunting rules **by default** for these collections:
> `attacks/ddos`, `attacks/phishing_group`, `attacks/phishing_kit`,
> `hi/open_threats`, `malware/config`, `osi/vulnerability`, and all
> `suspicious_ip/*` (open*proxy, scanner, socks_proxy, tor_node, vpn). For these,
> leaving the input on **`API default`** yields the \_filtered subset* — select
> **`Do not apply (0)`** if you want the full feed. The remaining collections
> (`apt/threat`, `apt/threat_actor`, `hi/threat`, `hi/threat_actor`,
> `compromised/breacheddb`) are unfiltered by default; select **`Apply (1)`** to
> filter them.

## Optional filters

Opt-in, per-collection filters. All default to "off"/"no filter" so the feed
behaves like a plain pull unless you set them. (`apply_hunting_rules` is its own
control — see **Hunting rules** above.)

| Input                                                 | Collection                | Values                                                                                                        | Effect                                                                           |
| ----------------------------------------------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `ioc_primary_q`                                       | ioc/primary               | `all` / `network` / `file`                                                                                    | Restrict to network- or file-type indicators. `all` = no filter.                 |
| `compromised_spd_type`                                | compromised/spd           | `all`, Cryptocurrency Wallet, Bank Account Number, Mobile number, IBAN, Bank card, Unknown, QR payment string | Filter Suspicious Payment Details to one payment-detail type. `all` = no filter. |
| `compromised_account_group_combolist`                 | compromised/account_group | Boolean                                                                                                       | On → restrict to combolist-sourced (credential-dump) accounts.                   |
| `compromised_account_group_probable_corporate_access` | compromised/account_group | Boolean                                                                                                       | On → restrict to accounts that likely grant corporate access.                    |
| `compromised_breacheddb_has_password`                 | compromised/breacheddb    | Boolean                                                                                                       | On → only breach records that include a password.                                |
| `malware_malware_with_description`                    | malware/malware           | `API default` / `true` / `false`                                                                              | Include/exclude the malware long description. `API default` = no parameter.      |

> `unique` is **always** applied to `compromised/account_group` (deduplicated
> accounts) — it is forced by the integration and is not an operator setting.

---

## Contact

In case of any problems, please, don't hesitate to contact Group-IB either through the email _intgeration@group-ib.com_ or submit a ticket to Group-IB Service Desk.
We would highly appreciate if you could attach relevant logs when reaching our regarding integration related issues.
