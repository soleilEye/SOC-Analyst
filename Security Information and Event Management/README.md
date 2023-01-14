# SIEM and Analyst Relationship

This will be generally about what SIEM is, why it is utilized within a SOC and the relationship between SIEM and a SOC analyst.

## What is SIEM?

Security information and event management (SIEM), is a security solution that provides the real time logging of events in an environment. The actual purpose for event logging is to detect security threats. It is a tool that collects data from various endpoints/network devices across the network, stores them at a centralized place, and performs correlation on them. The ones that interest us most as SOC analysts are: they filter the data that they collect and create alerts for any suspicious events.

<p align="center">
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Security%20Information%20and%20Event%20Management/Images/siem%20alert.png>
</p>

Example of an alert: If someone on a Windows operating system attempts to enter 20 incorrect passwords in 10 seconds, this is suspicious activity, it is not likely that someone who forgot their password would try to re-enter their password so many times in such a short period. This is why we create a SIEM rule/filter, to determine such activities that exceed the threshold values. Due to this SIEM rule an alert will be created if such a situation occurs.

## Network Visibility through SIEM

Before explaining the importance of SIEM, let's first understand why it is critical to have better visibility of all the activities within a network. The image below shows an example of a simple network that comprises multiple Linux/Windows based Endpoints, one data server, and one website. Each component communicates with the other or accesses the internet through a router.

<p align="center">
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Security%20Information%20and%20Event%20Management/Images/Scheme.png>
</p>

As we know, each network component can have one or more log sources generating different logs. One example could be setting up Sysmon along with Windows Event logs to have better visibility of Windows Endpoint. We can divide our network log sources into two logical parts:

1) Host-Centric Log Sources
These are log sources that capture events that occurred within or related to the host. Some log sources that generate host-centric logs are Windows Event logs, Sysmon, Osquery, etc. Some examples of host-centric logs are:

* A user accessing a file
* A user attempting to authenticate.
* A process Execution Activity
* A process adding/editing/deleting a registry key or value.
* Powershell execution

2) Network-Centric Log Sources
Network-related logs are generated when the hosts communicate with each other or access the internet to visit a website. Some network-based protocols are SSH, VPN, HTTP/s, FTP, etc. Examples of such events are:

* SSH connection
* A file being accessed via FTP
* Web traffic
* A user accessing company's resources through VPN.
* Network file sharing Activity

## Importance of SIEM
Now that we have covered various types of logs, it's time to understand the importance of SIEM. As all these devices generate hundreds of events per second, examining the logs on each device one by one in case of any incident can be a tedious task. That is one of the advantages of having a SIEM solution in place. It not only takes logs from various sources in real-time but also provides the ability to correlate between events, search through the logs, investigate incidents and respond promptly. Some key features provided by SIEM are:

* Real-time log Ingestion
* Alerting against abnormal activities
* 24/7 Monitoring and visibility
* Protection against the latest threats through early detection
* Data Insights and visualization
* Ability to investigate past incidents.

<p align="center">
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Security%20Information%20and%20Event%20Management/Images/SIEM.png>
</p>
