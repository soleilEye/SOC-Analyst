## Cisco Talos Intelligence

IT and Cybersecurity companies collect massive amounts of information that could be used for threat analysis and intelligence. Being one of those companies, Cisco assembled a large team of security practitioners called Cisco Talos to provide actionable intelligence, visibility on indicators, and protection against emerging threats through data collected from their products. The solution is accessible as Talos Intelligence.

Cisco Talos encompasses six key teams:

* **Threat Intelligence & Interdiction**: Quick correlation and tracking of threats provide a means to turn simple IOCs into context-rich intel.
* **Detection Research**: Vulnerability and malware analysis is performed to create rules and content for threat detection.
* **Engineering & Developmen**t: Provides the maintenance support for the inspection engines and keeps them up-to-date to identify and triage emerging threats.
* **Vulnerability Research & Discovery**: Working with service and software vendors to develop repeatable means of identifying and reporting security vulnerabilities.
* **Communities**: Maintains the image of the team and the open-source solutions.
* **Global Outreach**: Disseminates intelligence to customers and the security community through publications.


## Talos Dashboard
Accessing the open-source solution, we are first presented with a reputation lookup dashboard with a world map. This map shows an overview of email traffic with indicators of whether the emails are legitimate, spam or malware across numerous countries. Clicking on any marker, we see more information associated with IP and hostname addresses, volume on the day and the type.

<p align="center">
  <img src="https://github.com/AM1RKA/SOC-Analyst/blob/main/Cyber%20Threat%20Intellegence/Threat%20Intelligence%20Tools/Cisco%20Talos%20Intelligence/TalosWebsite.png">
</p>

At the top, we have several tabs that provide different types of intelligence resources. The primary tabs that an analyst would interact with are:

* **Vulnerability Information**: Disclosed and zero-day vulnerability reports marked with CVE numbers and CVSS scores. Details of the vulnerabilities reported are provided when you select a specific report, including the timeline taken to get the report published. Microsoft vulnerability advisories are also provided, with the applicable snort rules that can be used.

<p align="center">
  <img src="https://github.com/AM1RKA/SOC-Analyst/blob/main/Cyber%20Threat%20Intellegence/Threat%20Intelligence%20Tools/Cisco%20Talos%20Intelligence/Talos2.gif">
</p>

* **Reputation Center**: Provides access to searchable threat data related to IPs and files using their SHA256 hashes. Analysts would rely on these options to conduct their investigations. Additional email and spam data can be found under the Email & Spam Data tab.

<p align="center">
  <img src="https://github.com/AM1RKA/SOC-Analyst/blob/main/Cyber%20Threat%20Intellegence/Threat%20Intelligence%20Tools/Cisco%20Talos%20Intelligence/Talos3.gif">
</p>

<p align="center">
  <img src="https://github.com/AM1RKA/SOC-Analyst/blob/main/Cyber%20Threat%20Intellegence/Threat%20Intelligence%20Tools/Cisco%20Talos%20Intelligence/Talos4.gif">
</p>
