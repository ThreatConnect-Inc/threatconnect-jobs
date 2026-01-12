Group-IB Threat Intelligence 

User Documentation:
https://github.com/ThreatConnect-Inc/threatconnect-jobs/blob/master/apps/Group-IB%20Threat%20Intelligence/GIB_TI_ThreatConnect_User_Guide.pdf 


# Release Notes

## 1.0.0 (YYYY-MM-DD)
* Initial Release

## 1.0.1 (2021-02-21)
* Minor bugs fixes

## 1.0.2 (2021-03-26)
* Phishing IPs and Domains deprecation.

## 1.0.3 (2021-08-02)
* Malware CNC IPs attributes added(First Seen, Last Seen) + additional Malware name tags

## 1.0.4 (2023-03-25)
* Extra fields added to reports for the next collections: Threat, Threat Actor

## 1.2.0 (2024-02-22)
* Refactored connection logic
* Data ingestion logic update
* New collections added:
  * attacks/phishing_group
  * compromised/access
  * compromised/account_group
  * compromised/bank_card
  * compromised/masked_card
  * compromised/messenger
  * hi/open_threats
  * ioc/common
  * osi/git_repository
  * suspicious_ip/vpn
  * suspicious_ip/scanner
* Deprecated collections removed:
  * compromised/account
  * attacks/phishing
  * bp/phishing
  * bp/phishing_kit
  * malware/targeted_malware
  * osi/code_repository
* About 50 fields where added to old collections' objects

## 1.3.0 (2026-01-12)

<br>

# ThreatConnect Group-IB TI Integration Setup Guide

This document outlines the steps required to set up and configure the Group-IB Threat Intelligence integration with the ThreatConnect Platform.

---

## Before You Begin

Ensure the following prerequisites are met before starting the installation:

* **Supported Platform:** You must be running a **supported version of the ThreatConnect Platform**.
* **Application Pre-Check:** Verify that the **TC Group-IB TI application has been installed without errors** (if a previous attempt was made).
* **Credentials:** Make sure you have **valid Group-IB and ThreatConnect API credentials**.

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

1.  **Follow the instructions in the Configuration section in the extended documentation guide**  to create a new job for the app and begin data synchronization.

## Contact
In case of any problems, please, don't hesitate to contact Group-IB either through the email _intgeration@group-ib.com_ or submit a ticket to Group-IB Service Desk.
We would highly appreciate if you could attach relevant logs when reaching our regarding integration related issues. 