ChangeLog

1.2.0
- fix: delete hard coded app config
- convert from using tcex args to inputs

1.10 changelog for feed integration:
- update tcex package
- update polyswarm package
- use tcex v3 Malware type
- fix bug related to duplicate malware family names

User Guide: https://github.com/ThreatConnect-Inc/threatconnect-jobs/blob/master/apps/Polyswarm-Ransomware-Intelliegence/Polyswarm%20Ransomware%20Threat%20Intelligence%20Feed%20User%20Guide%20v1.0.pdf


## PolySwarm to ThreatConnect data conversion

### PolyScore -> Confidence
The PolySwarm PolyScore (0-1) is used to determine the ThreatConnect confidence level (1-100) for the indicator using the following formula.

$$  \lfloor polyscore*100 \rfloor $$


### Confidence -> Threat Rating
The confidence score is then used to calculate a threat rating (1-5) for the indicator.

$$  \lfloor confidence * 0.05 \rfloor $$