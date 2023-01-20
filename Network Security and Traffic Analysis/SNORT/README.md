<p align='center'>
  <img src=https://user-images.githubusercontent.com/80647611/213654342-ac60a7a3-d4cc-4a9b-a4f5-04be3f5f0995.png>
</p>

SNORT is an open-source, rule-based Network Intrusion Detection and Prevention System (NIDS/NIPS). It was developed and still maintained by Martin Roesch, open-source contributors, and the Cisco Talos team. 

**The official description:** *"Snort is the foremost Open Source Intrusion Prevention System (IPS) in the world. Snort IPS uses a series of rules that help define malicious network activity and uses those rules to find packets that match against them and generate alerts for users."*

# Introduction to IDS/IPS

<p align='center'>
  <img src=https://user-images.githubusercontent.com/80647611/213655552-813693b8-c5db-426d-b0cc-1219966660e1.png>
</p

Before diving into Snort and analysing traffic, let's have a brief overview of what an Intrusion Detection System (IDS) and Intrusion Prevention System (IPS) is. It is possible to configure your network infrastructure and use both of them, but before starting to use any of them, let's learn the differences.
  
## Intrusion Detection System (IDS)

IDS is a passive monitoring solution for detecting possible malicious activities/patterns, abnormal incidents, and policy violations. It is responsible for generating alerts for each suspicious event. 

### There are two main types of IDS systems;

* **Network Intrusion Detection System (NIDS)** - NIDS monitors the traffic flow from various areas of the network. The aim is to investigate the traffic on the entire subnet. If a signature is identified, an **alert is created.**
* **Host-based Intrusion Detection System (HIDS)** - HIDS monitors the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device. If a signature is identified, an **alert is created.**
  
## Intrusion Prevention System (IPS)
IPS is an active protecting solution for preventing possible malicious activities/patterns, abnormal incidents, and policy violations. It is responsible for stopping/preventing/terminating the suspicious event as soon as the detection is performed.

### There are four main types of IPS systems;

* **Network Intrusion Prevention System (NIPS)** - NIPS monitors the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If a signature is identified, the **connection is terminated.**
* **Behaviour-based Intrusion Prevention System (Network Behaviour Analysis - NBA)** - Behaviour-based systems monitor the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If a signature is identified, the **connection is terminated.**

Network Behaviour Analysis System works similar to NIPS. The difference between NIPS and Behaviour-based is; behaviour based systems require a training period (also known as "baselining") to learn the normal traffic and differentiate the malicious traffic and threats. This model provides more efficient results against new threats.

The system is trained to know the "normal" to detect "abnormal". The training period is crucial to avoid any false positives. In case of any security breach during the training period, the results will be highly problematic. Another critical point is to ensure that the system is well trained to recognise benign activities. 
  
* **Wireless Intrusion Prevention System (WIPS)** - WIPS monitors the traffic flow from of wireless network. The aim is to protect the wireless traffic and stop possible attacks launched from there. If a signature is identified, the **connection is terminated.**
* **Host-based Intrusion Prevention System (HIPS)** - HIPS actively protects the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device. If a signature is identified, the **connection is terminated.**

HIPS working mechanism is similar to HIDS. The difference between them is that **while HIDS creates alerts for threats, HIPS stops the threats by terminating the connection.**
  
## Detection/Prevention Techniques

There are three main detection and prevention techniques used in IDS and IPS solutions;

|Technique| Approach |
|-----------|---------|
| Signature-Based | This technique relies on rules that identify the specific patterns of the known malicious behaviour. This model helps detect known threats. |
| Behaviour-Based | This technique identifies new threats with new patterns that pass through signatures. The model compares the known/normal with unknown/abnormal behaviours. This model helps detect previously unknown or new threats. |
| Policy-Based | This technique compares detected activities with system configuration and security policies. This model helps detect policy violations. |
  
## Summary

Phew! That was a long ride and lots of information. Let's summarise the overall functions of the IDS and IPS in a nutshell.

* IDS can identify threats but require user assistance to stop them.
* IPS can identify and block the threats with less user assistance at the detection time.
  
Now let's talk about Snort. [Here is the rest of the official description](https://www.snort.org/) of the snort;

*"Snort can be deployed inline to stop these packets, as well. Snort has three primary uses: As a packet sniffer like tcpdump, as a packet logger — which is useful for network traffic debugging, or it can be used as a full-blown network intrusion prevention system. Snort can be downloaded and configured for personal and business use alike."*

SNORT is an **open-source**, **rule-based** Network Intrusion Detection and Prevention System (NIDS/NIPS). It was developed and still maintained by Martin Roesch, open-source contributors, and the Cisco Talos team. 

### Capabilities of Snort;

* Live traffic analysis
* Attack and probe detection
* Packet logging
* Protocol analysis
* Real-time alerting
* Modules & plugins
* Pre-processors
* Cross-platform support! (Linux & Windows)
<p align='center'>
  <img src=https://user-images.githubusercontent.com/80647611/213658887-6380eaff-29f7-4075-970c-bcdc467dd027.png>
</p>

### Snort has three main use models;

* **Sniffer Mode** - Read IP packets and prompt them in the console application.
* **Packet Logger Mode** - Log all IP packets (inbound and outbound) that visit the network.
* **NIDS (Network Intrusion Detection System)  and NIPS (Network Intrusion Prevention System) Modes** - Log/drop the packets that are deemed as malicious according to the user-defined rules.
