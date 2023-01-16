# Common Mistakes for SOC Analysts

Like any person, SOC analysts also make mistakes. In this section we will mention mistakes that are frequently made by SOC analysts and discuss how we can avoid making these mistakes ourselves.

* Overly Depending on VirusTotal Results
* Hasty Analysis of Malware in a Sandbox
* Insufficient Log Analysis
* Overlooking VirusTotal Dates

## Overly Depending on VirusTotal Results

Sometimes we can rely on the result displayed on VirusTotal’s green screen after analyzing a file’s URL and seeing that the address is harmless. But there is a new malicious software developed using an AV (AntiVirus) Bypass technique that may not be detected by VT (VirusTotal). For this reason we should accept VirusTotal as a supportive tool and conduct our analyses with this in mind.

Here’s a detailed blog post related to the subject for further reading: https://medium.com/maverislabs/virustotal-is-not-an-incident-responder-80a6bb687eb9

## Hasty Analysis of Malware in a Sandbox

A 3 to 4 minute analysis in a sandbox environment may not always produce accurate results. Here are the reasons:

* Malware that detects a sandbox environment and does not activate itself
* Malware that do not activate until 10-15 minutes after the operation

For this reason, the duration of analysis should be kept as long as possible and it should take place in a real environment if possible.

## Insufficient Log Analysis

From time to time we see that log analyses are not performed correctly. For example, let’s say that a piece of malware has detected a device with the hostname “LetsDefend” and this malware is secretly sending data to the address “letsdefend.io”. As a SOC analyst we should utilize “Log Management” solutions to determine whether any other device is trying to connect to this address.

## Overlooking VirusTotal Dates

If the search you have performed in VirusTotal has been queried before, a result from the cache will be displayed. For example: We searched the address “letsdefend.io” on VirusTotal and the result is below.
