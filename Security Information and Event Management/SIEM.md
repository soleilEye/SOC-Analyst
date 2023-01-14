# SIEM and Analyst Relationship

This will be generally about what SIEM is, why it is utilized within a SOC and the relationship between SIEM and a SOC analyst.

## What is SIEM?

Security information and event management (SIEM), is a security solution that provides the real time logging of events in an environment. The actual purpose for event logging is to detect security threats. It is a tool that collects data from various endpoints/network devices across the network, stores them at a centralized place, and performs correlation on them. The ones that interest us most as SOC analysts are: they filter the data that they collect.

<p align="center">
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Security%20Information%20and%20Event%20Management/Images/siem%20alert.png>
</p>

SIEM is used to provide correlation on the collected data to detect threats. Once a threat is detected, or a certain threshold is crossed, an alert is raised. This alert enables the analysts to take suitable actions based on the investigation. SIEM plays an important role in the Cyber Security domain and helps detect and protect against the latest threats in a timely manner. It provides good visibility of what's happening within the network infrastructure.

Example of an alert: If someone on a Windows operating system attempts to enter 20 incorrect passwords in 10 seconds, this is suspicious activity, it is not likely that someone who forgot their password would try to re-enter their password so many times in such a short period. This is why we create a SIEM rule/filter, to determine such activities that exceed the threshold values. Due to this SIEM rule an alert will be created if such a situation occurs.

Some popular SIEM solutions: IBM QRadar, ArcSight ESM, FortiSIEM, Splunk etc. 

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

SIEM tool gets all the security-related logs ingested through agents, port forwarding, etc. Once the logs are ingested, SIEM looks for unwanted behavior or suspicious pattern within the logs with the help of the conditions set in the rules by the analysts. If the condition is met, a rule gets triggered, and the incident is investigated.

## Relationship Between a SOC Analyst and SIEM

Although SIEM solutions have many features, as SOC analysts we generally only follow alerts. There are other groups/people who develop configurations and rule correlations.

As we mentioned above, alerts are created by data that is passed through filters. The alerts are primarily analyzed by a SOC analyst. This is exactly where a SOC analyst’s duty in the security operations center begins. Fundamentally, he/she must decide whether this created alert is a real threat or a false alarm.

As a SOC analyst we should analyze the details related to these alerts with the help of other SOC products (such as EDR, Log Management, Threat Intelligence Feed, etc.) and lastly we should determine whether or not they are real threats.

Let's dive into SIEM system's UI.

## Dashboard

Dashboards are the most important components of any SIEM. SIEM presents the data for analysis after being normalized and ingested. The summary of these analyses is presented in the form of actionable insights with the help of multiple dashboards. Each SIEM solution comes with some default dashboards and provides an option for custom Dashboard creation. Some of the information that can be found in a dashboard are:

* Alert Highlights
* System Notification
* Health Alert
* List of Failed Login Attempts
* Events Ingested Count
* Rules triggered
* Top Domains Visited
An example of a Default dashboard in Qradar SIEM is shown below:
<p align='centric'>
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Security%20Information%20and%20Event%20Management/Images/QRadarSIEM.png>
</p>

## Correlation Rules

Correlation rules play an important role in the timely detection of threats allowing analysts to take action on time. Correlation rules are pretty much logical expressions set to be triggered. A few examples of correlation rules are:

* If a User gets 5 failed Login Attempts in 10 seconds - Raise an alert for `Multiple Failed Login Attempts`
* If login is successful after multiple failed login attempts - Raise an alert for `Successful Login After multiple Login Attempts`
* A rule is set to alert every time a user plugs in a USB (Useful if USB is restricted as per the company policy)
* If outbound traffic is > 25 MB - Raise an alert to potential Data exfiltration Attempt (Usually, it depends on the company policy)

## How a correlation rule is created

To explain how the rule works, consider the following Eventlog use cases:

### Use-Case 1:

Adversaries tend to remove the logs during the post-exploitation phase to remove their tracks. A unique Event ID **104** is logged every time a user tries to remove or clear event logs. To create a rule based on this activity, we can set the condition as follows:

**Rule**: If the Log source is WinEventLog **AND** EventID is **104** - Trigger an alert `Event Log Cleared`

### Use-Case 2: 
Adversaries use commands like **whoami** after the exploitation/privilege escalation phase. The following Fields will be helpful to include in the rule.

* Log source: Identify the log source capturing the event logs
* Event ID: which Event ID is associated with Process Execution activity? In this case, event id **4688** will be helpful.
* NewProcessName: which process name will be helpful to include in the rule?
**Rule**: If Log Source is **WinEventLog** **AND** EventCode is **4688**, and NewProcessName contains **whoami**, then Trigger an `ALERT WHOAMI command Execution DETECTED`

Correlation rules keep an eye on the values of certain fields to get triggered. That is the reason why it is important to have normalized logs ingested.

## Alert Investigation

When monitoring SIEM, analysts spend most of their time on dashboards as it displays various key details about the network in a very summarized way. Once an alert is triggered, the events/flows associated with the alert are examined, and the rule is checked to see which conditions are met. Based on the investigation, the analyst determines if it's a True or False positive. Some of the actions that are performed after the analysis are:

* Alert is False Alarm. It may require tuning the rule to avoid similar False positives from occurring again.
* Alert is True Positive. Perform further investigation.
* Contact the asset owner to inquire about the activity.
* Suspicious activity is confirmed. Isolate the infected host.
* Block the suspicious IP.
