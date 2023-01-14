# Log Management
You will be doing a lot of log analysis as a SOC Analyst. For this reason, it is important to be familiar with “Log Management” systems/solutions. What brand product you use is not important, rather what’s important is knowing what to look for and where to look for it.


## What is Log Management?

As implied by its name, it is a log management solution. In short, it enables access to all the logs in an environment (web logs, operating system logs, Firewall, Proxy, EDR, etc.) and it allows for the management of these logs from one point. Thus, it improves usability and saves time.

If we can’t access the logs from one point, then the same query (for example I want to determine all users at letsdefend.io) would need to be sent to various devices. This would increase our margin of error and the amount of time we need to spend.

Every device in the network generates some kind of log whenever an activity is performed on it, like a user visiting a website, connecting to SSH, logging into his workstation, etc. Some common devices that are found in a network environment are discussed below:

## Windows Machine

Windows records every event that can be viewed through the Event Viewer utility. It assigns a unique ID to each type of log activity, making it easy for the analyst to examine and keep track of. To view events in a Windows environment, type `Event Viewer` in the search bar, and it takes you to the tool where different logs are stored and can be viewed, as shown below. These logs from all windows endpoints are forwarded to the SIEM solution for monitoring and better visibility.

<p align='center'>
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Security%20Information%20and%20Event%20Management/Images/EventViewer.gif>
</p>

## Linux Workstation

Linux OS stores all the related logs, such as events, errors, warnings, etc. Which are then ingested into SIEM for continuous monitoring. Some of the common locations where Linux store logs are:

* **/var/log/httpd** : Contains HTTP Request  / Response and error logs.
* **/var/log/cron**   : Events related to cron jobs are stored in this location.
* **/var/log/auth.log and /var/log/secure** : Stores authentication related logs.
* **/var/log/kern** : This file stores kernel related events.

Here is a sample of a cron log:
```log
May 28 13:04:20 ebr crond[2843]: /usr/sbin/crond 4.4 dillon's cron daemon, started with loglevel notice
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-hourly)
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-daily)
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-weekly)
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-monthly)
Jun 13 07:46:22 ebr crond[3592]: unable to exec /usr/sbin/sendmail: cron output for user root job sys-daily to /dev/null
```

## Web Server

It is important to keep an eye on all the requests/responses coming in and out of the webserver for any potential web attack attempt. In Linux, common locations to write all apache related logs are **/var/log/apache** or **/var/log/httpd**.

Here is an example of Apache Logs:
```log
192.168.21.200 - - [21/March/2022:10:17:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395
127.0.0.1 - - [21/March/2022:10:22:04 -0300] "GET / HTTP/1.0" 200 2216
```
## Log Ingestion

All these logs provide a wealth of information and can help in identifying security issues. Each SIEM solution has its own way of ingesting the logs. Some common methods used by these SIEM solutions are explained below:

1) Agent / Forwarder: These SIEM solutions provide a lightweight tool called an agent (forwarder by Splunk) that gets installed in the Endpoint. It is configured to capture all the important logs and send them to the SIEM server.

2) Syslog: Syslog is a widely used protocol to collect data from various systems like web servers, databases, etc., are sent real-time data to the centralized destination.
3) Manual Upload: Some SIEM solutions, like Splunk, ELK, etc., allow users to ingest offline data for quick analysis. Once the data is ingested, it is normalized and made available for analysis.

4) Port-Forwarding: SIEM solutions can also be configured to listen on a certain port, and then the endpoints forward the data to the SIEM instance on the listening port.

<p align='centric'>
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Security%20Information%20and%20Event%20Management/Images/SIEM2.png>
</p>
An example of how Splunk provides various methods for log Ingestion is shown below:
<p align='centric'>
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Security%20Information%20and%20Event%20Management/Images/Splunk.png>
</p>
