## SOC

This github repository contains links/tools that a cybersec specialist can use in his work. Some of the sites included might require install on your local machine or you can use docker 🐳

|Link        | Description           |
|:-------------:|:------------:| 
| [Cyber Defence Frameworks](https://github.com/AM1RKA/SOC-Analyst/tree/main/Cyber%20Defence%20Frameworks)   | Frameworks and policies that help establish a good security posture. | 
| [Cyber Threat Intellegence](https://github.com/AM1RKA/SOC-Analyst/tree/main/Cyber%20Threat%20Intellegence)  | About identifying and using available security knowledge to mitigate and manage potential adversary actions(`Yara`; `OpenCTI`; `MISP` and more...) |
| [Network Security and Traffic Analysis](https://github.com/AM1RKA/SOC-Analyst/tree/main/Network%20Security%20and%20Traffic%20Analysis)  | The core concepts of Network Security and Traffic Analysis to spot and probe network anomalies using industry tools and techniques such as `Snort`; `NetworkMiner`; `Zeek`; `Brim`; `Wireshark` |
| [Endpoint Security Monitoring](https://github.com/AM1RKA/SOC-Analyst/tree/main/Endpoint%20Security%20Monitoring)  | Monitoring activity on workstations is essential, as that’s where adversaries spend the most time trying to achieve their objectives. In this sections covers: `Core Windows Process`; `Sysinternals`; `Windows Event Logs`; `Sysmon`; `Osquery`; `Wazuh` | 
| [Security Information and Event Management](https://github.com/AM1RKA/SOC-Analyst/tree/main/Security%20Information%20and%20Event%20Management)   | How SIEM works and get comfortable creating simple and advanced search queries to look for specific answers from the ingested logs. SIEM's: _ELK; Splunk_ | 
| [Digital Forensics and Incident Response](https://github.com/AM1RKA/SOC-Analyst/tree/main/Digital%20Forensics%20and%20Incident%20Response) | What forensic artifacts are present in the Windows and Linux Operating Systems, how to collect them, and leverage them to investigate security incidents. `Windows/Linux Forensic`; `Autopsy`; `Redline`; `KAPE`; `Volatility`; `Velociraptor`; `TheHive Project`... |
| [Phishing](https://github.com/AM1RKA/SOC-Analyst/tree/main/Phishing) | Analyze and defend against phishing emails. Investigate real-world phishing attempts using a variety of techniques. |

This table will be updated with new entries. Links lead to my repositories, which will be created specifically for each topic. ✍(◔◡◔)

# SOC Types and Roles
## What is a SOC?
A Security Operation Center (SOC) is the facility where the information security team constantly monitors and analyzes the security of an organization. The main purpose of the SOC team is to detect, analyze and respond to cyber security incidents by using technology, people and processes.

## Types Of SOC Models
Depending on security requirements and budget, there are several types of SOC:

### In-house SOC
The enterprise builds its own cybersecurity team. Firms considering establishing an internal SOC should have a budget to support continuity.

### Virtual SOC
The security team does not have its own facility and often works remotely in different locations.

### Co-Managed SOC
The Co-Managed SOC consists of internal SOC personnel working with an external Managed Security Service Provider (MSSP). The coordination is really important for this type of model.

### Command SOC
A senior group that oversees smaller SOCs in a large region. Organizations using this model include major telecom providers and defense agencies.

## People, Process and Technology

Building a successful SOC requires serious coordination. In particular, there should be a strong relationship between people, processes, and technologies.
In simple terms, we will talk about which people, processes and technologies are required for SOC.

### People
We need highly trained personnel familiar with security alerts and attack scenarios. As attack types are constantly changing, we need a teammate that can easily adapt to new attack types and is willing to research.

### Processes
To bring your SOC structure to good maturity, you need to equal it with many different types of security requirements such as NIST, PCI, HIPAA. Processes require extreme standardization of actions to ensure nothing is skipped.

### Technology
You need to have various products for many topics such as penetration test, detection, prevention, analyze. You need to follow the market and technology closely to find the best solution for you. Sometimes the best product on the market may not be the best for you. This may be due to your low budget.

## SOC Positions

### SOC Analyst
It can be divided into groups as Level 1, 2 and 3 according to the SOC structure. A security analyst classifies the alert, looks for the cause, and advises on remedial measures.

### Incident Responder
The incident response officer is the person who will take part in threat detection. This person performs the initial assessment of security breaches.

### Threat Hunter
A team member whose purpose is to find vulnerabilities before the attacker can exploit them with an attack.

### Security Engineer
Security Engineers maintain the security infrastructure of SIEM (Security Information and Event Management) solutions and SOC products. For example, this person prepares the connection between SIEM and SOAR (Security orchestration, automation and response) product.

### SOC Manager
A SOC Manager takes on management responsibilities such as budgeting, strategizing, managing personnel and coordinating operations. He/She deals with operational rather than technical matters.

## SOC Analyst and Their Responsibilities
In this section we will discuss what a SOC analyst is, his place in the SOC and what kind of work-related responsibilities he/she has in a general sense. It is important to read these sections carefully before learning about the technical side of things, this way candidates who desire to be SOC analysts can visualize what their future career would be like.

A SOC analyst is the first person to analyze any threats against a system. When the situation requires it, he/she escalates incidents to his seniors and thus makes catching threats possible. He/She plays an important role in the SOC because he/she is the first person to investigate.

### The Advantages of Being a SOC Analyst

There are many various techniques of attack vectors and malicious software and they increase more and more every day. As an analyst you will get greater enjoyment from investigating these varying types of incidents. Even though the operating systems, security products…etc. that you use will be the same the job will feel less monotonous because you will be analyzing different incidents. Also, you may not encounter such techniques (not every week or every day).

### General Routine

Throughout the day a SOC analyst will generally examine alerts on the SIEM and determine which ones are real threats. To reach a conclusion he/she will utilize various security products such as EDR (Endpoint Detection and Response), Log Management and SOAR. We will explain in detail why and how these products are used later.

To be a successful SOC analyst who is not dependent on security products and can correctly analyze SIEM alerts one needs to have the following competencies.

### Operating Systems

To be able to detect what is abnormal in a system one must primarily know what is accepted as normal. For example, there are multiple services within the Windows operating system and it is hard to detect which of these are suspicious without knowing which are or could be normal Windows services. For this reason, you should know the basic logic of how Windows/Linux operating systems work.

### Network

First and foremost, we will be handling many malicious IPs and URL addresses. And we will have to check if there are any devices on the network trying to connect to these addresses. If we can control this then it will set the tone of our analysis.

As a more complicated step we might have to detect a potential data leak on the network. To be able to carry out all these functions we need to know the basics of networking.

### Malware Analysis

You will come across some kind of malicious software when dealing with most threats. In order to be able to understand what the actual purpose of these malwares are (they sometimes display different behaviors to mislead analysts) you need to have some skills in malware analysis.

It is important to at least determine what the malicious file’s command and control center is and whether or not there is a device communicating with this address.
