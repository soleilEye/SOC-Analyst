<p align="center">
  <img src="https://user-images.githubusercontent.com/80647611/216758459-3529bd54-dc5f-4cd4-becd-979c3e6e03e4.png">
</p>

**NetworkMiner is an open-source traffic sniffer, pcap handler and protocol analyser. Developed and still maintained by Netresec.**

**The official description:**

*"NetworkMiner is an open source Network Forensic Analysis Tool (NFAT) for Windows (but also works in Linux / Mac OS X / FreeBSD). NetworkMiner can be used as a passive network sniffer/packet capturing tool to detect operating systems, sessions, hostnames, open ports etc. without putting any traffic on the network. NetworkMiner can also parse PCAP files for off-line analysis and to regenerate/reassemble transmitted files and certificates from PCAP files.
NetworkMiner makes it easy to perform advanced Network Traffic Analysis (NTA) by providing extracted artefacts in an intuitive user interface. The way data is presented not only makes the analysis simpler, it also saves valuable time for the analyst or forensic investigator.*

## NetworkMiner in a Nutshell

| Capability | Description |
| ----- | ------ |
| Traffic sniffing | It can intercept the traffic, sniff it, and collect and log packets that pass through the network. |
| Parsing PCAP files | It can parse pcap files and show the content of the packets in detail. |
| Protocol analysis | It can identify the used protocols from the parsed pcap file. |
| OS fingerprinting | It can identify the used OS by reading the pcap file. This feature strongly relies on Satori and p0f. |
| File Extraction | It can extract images, HTML files and emails from the parsed pcap file. |
| Credential grabbing | It can extract credentials from the parsed pcap file. |
| Clear text keyword parsing | It can extract cleartext keywords and strings from the parsed pcap file. |

## Operating Modes

There are two main operating modes;

* **Sniffer Mode:** Although it has a sniffing feature, it is not intended to use as a sniffer. The sniffier feature is available only on Windows. However, the rest of the features are available in Windows and Linux OS. Based on experience, the sniffing feature is not as reliable as other features. Therefore we suggest not using this tool as a primary sniffer. Even the official description of the tool mentions that this tool is a "Network Forensics Analysis Tool", but it can be used as a "sniffer". In other words, it is a Network Forensic Analysis Tool with but has a sniffer feature, but it is not a dedicated sniffer like Wireshark and tcpdump. 
* **Packet Parsing/Processing:** NetworkMiner can parse traffic captures to have a quick overview and information on the investigated capture. This operation mode is mainly suggested to grab the "low hanging fruit" before diving into a deeper investigation.


## Pros and Cons
 
As mentioned in the previous task, NetworkMiner is mainly used to gain an overview of the network. Before starting to investigate traffic data, let's look at the pros and cons of the NetworkMiner.

### Pros
* **OS fingerprinting**
* **Easy file extraction**
* **Credential grabbing**
* **Clear text keyword parsing**
* **Overall overview**

### Cons

* **Not useful in active sniffing**
* **Not useful for large pcap investigation**
* **Limited filtering**
* **Not built for manual traffic investigation**

# There are a few things to remember about the NetworkMiner;

* **Don't use this tool as a primary sniffer.**
* **Use this tool to overview the traffic, then move forward with Wireshark and tcpdump for a more in-depth investigation.**
