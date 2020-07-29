# PostMortem/Root Cause Analysis for AES EDI | JIRA Issue ( AESEDI-53447) 

## Date
2020-29-07

## Authors
*Sunil Yadav*
*Operations Team*

## Status
Resolved.

## Summary
The customer data was not sent from AES EDI. The investigation showed that the file with the data was sent however, it did not get processed due to an issue with the AES CIS service.

## Impact
About 486,000 records were affected and the EDI to CIS monitoring service.

## Root Causes
Sending files with a large number of records while simultaneously running the patching script caused a wreck in the data processing. This issue with AES CIS service futher escalated to data not getting processed leading to missing records.

## Resolution
Reloading the *AES CIS* monitoring service allowed us to spot the missed records that were not discovered automatically. Following this the data file was resent leading to the resolution.

## Detection
Customer created a Jira Ticket to alert us on this failure. *Please refer JIRA Issue: (AESEDI-53447)*


## Action Items
| Action Item | Type | Owner | Bug |
| ----------- | ---- | ----- | --- |
| Writing of monitoring policy to detect records missings | prevent | Sunil Yadav | **DONE** |
| Monitor the data ingesters and processors (ETL) | prevent | Sunil Yadav | (Jira Issue No: AESCIS-38263)**TODO** |

## Lessons Learned
1. More monitoring plugins and modules to watch this critical part of our infrastructure. 
2. Patching opearations should not be executed while data processing is in progress at AES EDI.

## Timeline

2020-29-07 (*all times UTC*)

| Time  | Description |
| ----- | ----------- |
| 11:56 | Discovering of the missing files |
| 12:00 | Restarting of the AES CIS monitoring module |
| 12:15 | Starting of the data processing of the records files |
| 13:00 | Completion of the data processing of all the 486,000 records files |
