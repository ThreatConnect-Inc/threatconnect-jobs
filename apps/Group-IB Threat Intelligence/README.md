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

## 1.3.0 (2025-12-18)

### New Features
- **Replaced Compromised Data :: Mules with Compromised Data :: SPD (Suspicious Payment Details)**: The `compromised_mule` collection has been replaced with `compromised_spd` to better reflect the nature of the data. 
- **Enhanced Compromised Data :: Accounts filtering**: Added three new filter flags for the `compromised_account_group` collection:
  - **Is in combolist?** (`compromised_account_group_combo`):  Filter accounts detected as a part of combolists
  - **Is a unique record?** (`compromised_account_group_unique`): Filter for accounts from unique detection records
  - **Filter for probable corporate access?** (`compromised_account_group_corp`): Filter accounts with probable corporate access indicators

### Improvements
- **Batch submission logic**: Fixed and improved batch submission logic to enhance data processing efficiency and reliability
- **Code refactoring**: Major code refactoring and improvements for better maintainability and code quality
- **Error handling**: Enhanced error handling and logging throughout the application for better debugging and monitoring
- **Documentation**: 
  - Improved overall documentation and user guidance
- **Attributes**: Updated attribute definitions and mappings to support new data types and improve data accuracy
