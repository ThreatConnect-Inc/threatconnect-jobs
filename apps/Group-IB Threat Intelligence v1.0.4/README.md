Group-IB Threat Intelligence 

User Documentation:
https://github.com/ThreatConnect-Inc/threatconnect-jobs/blob/master/apps/Group-IB%20Threat%20Intelligence/TC_GroupIB_TI_v1.2.x_for_ThreatConnect_TIP.pdf 


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
