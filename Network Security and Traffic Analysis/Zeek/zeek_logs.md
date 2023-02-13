<p align='center'>
  <img src=https://user-images.githubusercontent.com/80647611/216930199-11ff4dee-f9ca-44f3-af60-ff3de7ef7299.png>
</p>

# Zeek Logs
Zeek generates log files according to the traffic data. You will have logs for every connection in the wire, including the application level protocols and fields. Zeek is capable of identifying 50+ logs and categorising them into seven categories. Zeek logs are well structured and tab-separated ASCII files, so reading and processing them is easy but requires effort. You should be familiar with networking and protocols to correlate the logs in an investigation, know where to focus, and find a specific piece of evidence.

Each log output consists of multiple fields, and each field holds a different part of the traffic data. Correlation is done through a unique value called "UID". The "UID" represents the unique identifier assigned to each session.

## Zeek logs in a nutshell
| Category | Description | Log Files |
| ---------- | ------------ | ----------- |
Network | Network protocol | logs. conn.log, dce_rpc.log, dhcp.log, dnp3.log, dns.log, ftp.log, http.log, irc.log, kerberos.log, modbus.log, modbus_register_change.log, mysql.log, ntlm.log, ntp.log, radius.log, rdp.log, rfb.log, sip.log, smb_cmd.log, smb_files.log, smb_mapping.log, smtp.log, snmp.log, socks.log, ssh.log, ssl.log, syslog.log, tunnel.log. |
Files | File analysis result logs. | files.log, ocsp.log, pe.log, x509.log. |
NetControl |  Network control and flow logs. | netcontrol.log, netcontrol_drop.log, netcontrol_shunt.log, netcontrol_catch_release.log, openflow.log. |
Detection | Detection and possible indicator logs. | intel.log, notice.log, notice_alarm.log, signatures.log, traceroute.log. |
Network Observations | Network flow logs. | known_certs.log, known_hosts.log, known_modbus.log, known_services.log, software.log. |
Miscellaneous | Additional logs cover external alerts, inputs and failures. | barnyard2.log, dpd.log, unified2.log, unknown_protocols.log, weird.log, weird_stats.log. |
Zeek Diagnostic | Zeek diagnostic logs cover system messages, actions and some statistics. | broker.log, capture_loss.log, cluster.log, config.log, loaded_scripts.log, packet_filter.log, print.log, prof.log, reporter.log, stats.log, stderr.log, stdout.log. |

Please refer to [Zeek's official documentation](https://docs.zeek.org/en/current/script-reference/log-files.html) and [Corelight log cheat sheet](https://corelight.com/products/zeek-data/) for more information. Although there are multiple log files, some log files are updated daily, and some are updated in each session. Some of the most commonly used logs are explained in the given table.
| Update Frequency | Log Name | Description |
| ---------- | ------------ | ----------- |
Daily |	known_hosts.log |	List of hosts that completed TCP handshakes. |
Daily |	known_services.log |	List of services used by hosts. |
Daily |	known_certs.log	|	List of SSL certificates. |
Daily |	software.log |	List of software used on the network. |
Per Session |	notice.log	|	Anomalies detected by Zeek. |
Per Session | intel.log |	Traffic contains malicious patterns/indicators. |
Per Session | signatures.log |	List of triggered signatures. |

This is too much protocol and log information! Yes, it is true; a difficulty of working with Zeek is having the required network knowledge and investigation mindset.

| Overall Info | Protocol Based | Detection | Observation |
| ---------- | ------------ | ----------- | -------------- |
| conn.log | http.log |	notice.log |	known_host.log |
| files.log |	dns.log |	signatures.log |	known_services.log |
| intel.log |	ftp.log |	pe.log |	software.log |
| loaded_scripts.log |	ssh.log |	traceroute.log |	weird.log |

You can categorise the logs before starting an investigation. Thus, finding the evidence/anomaly you are looking for will be easier. The given table is a brief example of using multiple log files. You can create your working model or customise the given one. Make sure you read each log description and understand the purpose to know what to expect from the corresponding log file. Note that these are not the only ones to focus on. Investigated logs are highly associated with the investigation case type and hypothesis, so do not just rely only on the logs given in the example table!

The table shows us how to use multiple logs to identify anomalies and run an investigation by correlating across the available logs.

* **Overall Info:** The aim is to review the overall connections, shared files, loaded scripts and indicators at once. This is the first step of the investigation.
* **Protocol Based:** Once you review the overall traffic and find suspicious indicators or want to conduct a more in-depth investigation, you focus on a specific protocol.
* **Detection:** Use the prebuild or custom scripts and signature outcomes to support your findings by having additional indicators or linked actions. 
* **Observation:** The summary of the hosts, services, software, and unexpected activity statistics will help you discover possible missing points and conclude the investigation.

Remember, we mention the pros and cons of the Zeek logs at the beginning of this task. Now let's demonstrate the log viewing and identify the differences between them.

* **Recall 1:** Zeek logs are well structured and tab-separated ASCII files, so reading and processing them is easy but requires effort.
* **Recall 2:** Investigating the generated logs will require command-line tools (cat, cut, grep sort, and uniq) and additional tools (zeek-cut). 

![image](https://user-images.githubusercontent.com/80647611/218477141-07a22030-214c-4403-8b65-47b682998490.png)

The above image shows that reading the logs with tools is not enough to spot an anomaly quickly. Logs provide a vast amount of data to investigate and correlate. You will need to have technical knowledge and event correlation ability to carry out an investigation. It is possible to use external visualisation and correlation tools such as ELK and Splunk. We will focus on using and processing the logs with a hands-on approach in this room.

In addition to Linux command-line tools, one auxiliary program called `zeek-cut` reduces the effort of extracting specific columns from log files. Each log file provides "field names" in the beginning. This information will help you while using `zeek-cut`. Make sure that you use the "fields" and not the "types".
