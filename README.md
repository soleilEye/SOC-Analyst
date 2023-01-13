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
To bring your SOC structure to good maturity, you need to align it with many different types of security requirements such as NIST, PCI, HIPAA. Processes require extreme standardization of actions to ensure nothing is skipped.

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
