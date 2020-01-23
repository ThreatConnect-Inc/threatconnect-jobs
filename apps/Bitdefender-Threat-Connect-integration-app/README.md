# Introduction
**Bitdefender Advanced Threat Intelligence** is a  security service that enables security professionals to make more informed decisions by providing real-time threat knowledge that can be easily integrated in their existing technology stack.  The solution delivers up-to-date,  contextual intelligence on URLs, IPs, domains, certificates, files, Command and Control servers and Advanced Persistent Threats to Security Operation Centers (SOCs), Managed Security Service Providers (MSSPs), Managed Detection & Response (MDR) companies, IT security and investigation consultancies and large enterprises that need to block ingenious threats.

Bitdefender offers the following feeds as part of its offering:

 - **APT-IPs-feed** - *Feed of IPs associated with Advanced Persistent Threats*  
 - **APT-filehashes-feed** - *Feed of file hashes associated with Advanced Persistent Threats*  
 - **CNC-IPs-feed** - *Feed of IPs associated with command-and-control servers*  
 - **Phishing domains** – *Feed with domain addresses that are known to be associated to phishing attacks*  
 - **Malware domains** - *Feed with domain addresses that are known to be associated with malware*

This document describes how to integrate the Bitdefender Advanced Threat Intelligence service with the ThreatConnect Platform. Once the integration is successful, the IOCs provided by Bitdefender Advanced Threat Intelligence service will be visible in the ThreatConnect platform and ready for usage.

# App installation

## Requirements
Before proceeding with the installation, please ensure the following items are already available:

 - Access to ThreatConnect instance  
 - At least one ThreatConnect API user (See [Creating User Accounts](https://kb.threatconnect.com/customer/en/portal/articles/2188549-creating-user-accounts))  
 - Bitdefender Authentication Token . This is  provided by Bitdefender and it is used for authentication when connecting to Bitdefender Advanced Threat Intelligence services

## Installation
Bitdefender Advanced Threat  Intelligence app for ThreatConnect is available on Github at: [Github Link](https://github.com/ThreatConnect-Inc/threatconnect-jobs/tree/master/apps/Bitdefender-Advanced%20Threat%20Intelligence). Download the app package (represented by the file with the *tcx* extension and install it in your instance. 

> The steps required to install the app are outlined in the
> ThreatConnect System   Administration Guide (Install an App and Feed
> Deployer).   Additionally, for more information you can contact your
> ThreatConnect Customer Success   Engineer

## Attributes configuration

## ThreatConnect Job Configuration

> **Note:** This step is not required for users who use Feed Deployer as it is automatically performed by the Feed Deployer Wizard

The ThreatConnect Platform provides the ability for customers to schedule applications as jobs, specifically known as Job apps, that can  
be run at configured intervals. Bitdefender has developed a Job app for ThreatConnect customers by the name of Bitdefender Threat Intelligence that handles the complete process of downloading and ingesting the threat feed into the ThreatConnect Platform. In  
order to configure the Bitdefender job, follow the steps mentioned below:

 1. In your ThreatConnect console, navigate to the gear-icon on the top menu bar. From the drop-down menu, click on **Org Settings**
 2. Select the **Apps** tab , then click on the small `+` icon to add a new job
 3. Enter a name for the **Job** name (e.g. *Bitdefender Daily download*). From the **Run Program** drop-down list select **Bitdefender Threat Intelligence** . Press **Next** to proceed to the next configuration screen
 
 > **Note:** If you cannot see **Bitdefender Threat Intelligence** listed as an option, double check the App Installation step above or  contact your Customer Success Engineer
 > 
 4. In the next screen configure the Job parameters as follows:
	 * **Bitdefeder API key** : The auth token that was provided by your Bitdefender representative. If you do not have an API key, send an email to oem-sales@bitdefender.com
	 * **Feed Type** : choose the feeds for which you want data to be downloaded. The feed description can be found in the previous section - ***Introduction***
	 * **Hash type** : for each file indicators, specify the hash type you want to be added. Currently for each file indicator, MD5, SHA1 and SHA256 are available as hash types. If there is a need to have multiple hashes available for each file indicator, recreate a new job and specify a different hash value
	 * **Threat Rating** : set  the default *Threat Rating* assigned by ThreatConnect Platform to the imported indicators
	 *  **Confidence level** : modify the *Confidence* score assigned to imported indicators
	 * **Log level** : specify the Job log level. Useful when debugging the job execution
	 * **ThreatConnect Owner** : select Bitdefender Threat Intelligence as the owner of imported data.
 5. Press **Next** to move to the next screen where options regarding job schedule can be configured:
 > **Note:** For Confidence level, we recommend leaving a value of 100 due to the low rate of false-positive it is expected to be returned by the  Bitdefender Threat Intelligence feeds

> **Note**: Bitdefender recommends configuring the job to run on a 1h interval to ensure that the latest data is fed in the ThreatConnect platform

 7. Finally, press **Next** to configure **Notifications** about job execution
 8. Press **Save** to store the job in the ThreatConnect platform

The new job created should be listed in the **Jobs** list table. The job will not run until it is marked as active. 

> To activate the job, move the slider in the right direction. 
> 

> 
> **Note**: Data will  start flowing in the ThreatConnect Platform either when the scheduled time is met or when a manual trigger is performed. To trigger manually the job, go the Job previously defined and click the **Run Job** button located in the *Options* column

## Indicator deprecation configuration
From time to time, Bitdefender retires indicators in its threat feed that it estimates are, no longer malicious and pose any significant threat.  

These indicators previously ingested into the ThreatConnect Platform should also be deleted accordingly to avoid false-positives.  ThreatConnect provides the ability for users to configure an indicator deprecation policy to allow ThreatConnect indicators to drop in   confidence rating if their confidence rating is not being maintained and updated. Once the indicator rating reaches a minimum value (i.e.  
0%), it can either be set to inactive or delete. 

To configure an indicator deprecation policy depending upon the type of your ThreatConnect instance, please refer to the detailed knowledge-base article from ThreatConnect: [CONFIGURING INDICATOR CONFIDENCE  
DEPRECATION](https://kb.threatconnect.com/customer/en/portal/articles/2239026-configuring-indicator-confidence-deprecation) (See section Configuring Indicator Confidence Deprecation for an Organization and Configuring Indicator Confidence Deprecation for a Community or Source)  

The recommended indicator deprecation rule settings for Bitdefender threat feed are as follows:  

 - **Action at Minimum** selected to be **Delete** so that indicators are deleted as soon as they reach minimum confidence  
 - **Percentage** checkbox checked which means that indicator confidence will be dropped as a percent of its previous  
value  
- **Confidence** amount set to 100 so that 100% of an indicator's confidence is dropped
- **Interval** value set to 1 day which is the period after which the confidence *emphasized text*will be dropped  
- **Recurring** checkbox also selected so that deprecation is performed on a recurring basis  

In simple words the recommended deprecation rule can be stated as, "*After every day, drop the confidence of each indicator by   100% of its previous value and when any indicator's confidence reaches the minimum value, delete it from ThreatConnect"*

# Viewing and filtering the data
To view the data, click on **Browse** button located in the top menu of ThreatConnect console. From here, there are two options: either filter by selecting a specific **Indicator** or by searching for a specific **Indicator** name .

The mapping between Bitdefender feed data and the Indicators and Tags that are added in ThreatConnect can be observed in the table 

|Feed name| Indicator type | Tag
|--|--|--|
| APT File IP  |  Address | apt-ip
| APT File feed | File | apt-file
| C&C IP | Address| c2-ip
| Phishing Domains | Host | phishing-domains
| Malware Domains | Host | malware-domains
