![image](https://user-images.githubusercontent.com/80647611/214537587-bb67ff05-264d-459f-a223-2af0ddbb9cba.png)

# Let's Learn Snort Rules!

Understanding the Snort rule format is essential for any blue and purple teamer.  The primary structure of the snort rule is shown below;
![image](https://user-images.githubusercontent.com/80647611/214540291-c5c9f95e-08f1-411b-a8a4-83076752d475.png)

Each rule should have a type of action, protocol, source and destination IP, source and destination port and an option. Remember, Snort is in passive mode by default. So most of the time, you will use Snort as an IDS. You will need to start **"inline mode" to turn on IPS mode.** But before you start playing with inline mode, you should be familiar with Snort features and rules.

The Snort rule structure is easy to understand but difficult to produce. You should be familiar with rule options and related details to create efficient rules. It is recommended to practice Snort rules and option details for different use cases.

We will cover the basic rule structure in this room and help you take a step into snort rules. You can always advance your rule creation skills with different rule options by practising different use cases and studying rule option details in depth. We will focus on two actions; "alert"  for IDS mode and "reject" for IPS mode.

Rules cannot be processed without a header. Rule options are "optional" parts. However, it is almost impossible to detect sophisticated attacks without using the rule options.

|   | Desc |
| -------- | ---------|
| Action | There are several actions for rules. Make sure you understand the functionality and test it before creating rules for live systems. The most common actions are listed below. alert: Generate an alert and log the packet. log: Log the packet. drop: Block and log the packet. reject: Block the packet, log it and terminate the packet session. |
| Protocol | Protocol parameter identifies the type of the protocol that filtered for the rule. Note that Snort2 supports only four protocols filters in the rules (IP, TCP, UDP and ICMP). However, you can detect the application flows using port numbers and options. For instance, if you want to detect FTP traffic, you cannot use the FTP keyword in the protocol field but filter the FTP traffic by investigating TCP traffic on port 21. |

## IP and Port Numbers

These parameters identify the source and destination IP addresses and associated port numbers filtered for the rule.
|   | Desc |
| -------- | ---------|
| IP Filtering | **alert icmp 192.168.1.56 any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;).** This rule will create alerts for each ICMP packet originating from the 192.168.1.56 IP address. |
| Filter an IP range | **alert icmp 192.168.1.0/24 any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;).** This rule will create alerts for each ICMP packet originating from the 192.168.1.0/24 subnet. |
| Filter multiple IP ranges | **alert icmp [192.168.1.0/24, 10.1.1.0/24] any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;).** This rule will create alerts for each ICMP packet originating from the 192.168.1.0/24 and 10.1.1.0/24 subnets.|
| Exclude IP addresses/ranges | "negation operator" is used for excluding specific addresses and ports. Negation operator is indicated with "!" **alert icmp !192.168.1.0/24 any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;).** This rule will create alerts for each ICMP packet not originating from the 192.168.1.0/24 subnet. |
| Port Filtering | 	**alert tcp !192.168.1.0/24 21 <> any any  (msg: "TCP(FTP) Packet Found"; sid: 100001; rev:1;).** This rule will create alerts for each TCP packet originating from port 21. |
| Exclude a specific port | **alert tcp !192.168.1.0/24 !21 <> any any  (msg: "TCP(FTP) Packet Found"; sid: 100001; rev:1;)**. This rule will create alerts for each TCP packet not originating from port 21. |
| Filter a port range (Type 1)| **alert tcp !192.168.1.0/24 1:1024 <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;).** This rule will create alerts for each TCP packet originating from ports between 1-1024. |
| Filter a port range (Type 2) | **alert icmp any :1024 <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;).** This rule will create alerts for each ICMP packet originating from ports less than or equal to 1024. |
| Filter a port range (Type 3) | **alert icmp any 1024: <> any any (msg: "ICMP Packet Found"; sid: 100001; rev:1;).** This rule will create alerts for each ICMP packet originating from a source port higher than or equal to 1024. |
| Filter a port range (Type 4) | **alert icmp any 80,1024: <> any any (msg: "ICMP Packet Found"; sid: 100001; rev:1;).** This rule will create alerts for each ICMP packet originating from a source port 80 and higher than or equal to 1024. |

## Direction

The direction operator indicates the traffic flow to be filtered by Snort. The left side of the rule shows the source, and the right side shows the destination.

* **->** Source to destination flow.
* **<>** Bidirectional flow

**Note that there is no "<-" operator in Snort.**
![image](https://user-images.githubusercontent.com/80647611/214543507-9e4ba839-813f-4edb-833b-8552ff8ded39.png)

## There are three main rule options in Snort;

* **General Rule Options -** Fundamental rule options for Snort. 
* **Payload Rule Options -** Rule options that help to investigate the payload data. These options are helpful to detect specific payload patterns.
* **Non-Payload Rule Options -** Rule options that focus on non-payload data. These options will help create specific patterns and identify network issues.

## General Rule Options

|   | Desc |
| -------- | ---------|
| Msg | The message field is a basic prompt and quick identifier of the rule. Once the rule is triggered, the message filed will appear in the console or log. Usually, the message part is a one-liner that summarises the event. |
| Sid | Snort rule IDs (SID) come with a pre-defined scope, and each rule must have a SID in a proper format. There are three different scopes for SIDs shown below. **<100:** Reserved rules **100-999,999:** Rules came with the build. **>=1,000,000:** Rules created by user. Briefly, the rules we will create should have sid greater than 100.000.000. Another important point is; SIDs should not overlap, and each id must be unique. |
| Reference | Each rule can have additional information or reference to explain the purpose of the rule or threat pattern. That could be a Common Vulnerabilities and Exposures (CVE) id or external information. Having references for the rules will always help analysts during the alert and incident investigation. |
| Rev | Snort rules can be modified and updated for performance and efficiency issues. Rev option help analysts to have the revision information of each rule. Therefore, it will be easy to understand rule improvements. Each rule has its unique rev number, and there is no auto-backup feature on the rule history. Analysts should keep the rule history themselves. Rev option is only an indicator of how many times the rule had revisions. **alert icmp any any <> any any (msg: "ICMP Packet Found"; sid: 100001; reference:cve,CVE-XXXX; rev:1;)** |

## Payload Detection Rule Options

| | Desc |
| -------- | ---------|
| Content | Payload data. It matches specific payload data by ASCII, HEX or both. It is possible to use this option multiple times in a single rule. However, the more you create specific pattern match features, the more it takes time to investigate a packet. Following rules will create an alert for each HTTP packet containing the keyword "GET". This rule option is case sensitive! ASCII mode - **alert tcp any any <> any 80  (msg: "GET Request Found"; content:"GET"; sid: 100001; rev:1;)** HEX mode - alert tcp any any <> any 80  (msg: "GET Request Found"; content:"|47 45 54|"; sid: 100001; rev:1;) |
| Nocase | Disabling case sensitivity. Used for enhancing the content searches. **alert tcp any any <> any 80  (msg: "GET Request Found"; content:"GET"; nocase; sid: 100001; rev:1;)** |
| Fast_pattern | Prioritise content search to speed up the payload search operation. By default, Snort uses the biggest content and evaluates it against the rules. "fast_pattern" option helps you select the initial packet match with the specific value for further investigation. This option always works case insensitive and can be used once per rule. Note that this option is required when using multiple "content" options. The following rule has two content options, and the fast_pattern option tells to snort to use the first content option (in this case, "GET") for the initial packet match. **alert tcp any any <> any 80  (msg: "GET Request Found"; content:"GET"; fast_pattern; content:"www";  sid:100001; rev:1;)** |

## Non-Payload Detection Rule Options

There are rule options that focus on non-payload data. These options will help create specific patterns and identify network issues.

| | Desc |
| -------- | ---------|
| ID | Filtering the IP id field. **alert tcp any any <> any any (msg: "ID TEST"; id:123456; sid: 100001; rev:1;)** |
| Flags | Filtering the TCP flags. F - FIN S - SYN R - RST P - PSH A - ACK U - URG **alert tcp any any <> any any (msg: "FLAG TEST"; flags:S;  sid: 100001; rev:1;)** |
| Dsize | Filtering the packet payload size. dsize:min<>max; dsize:>100 dsize:<100 **alert ip any any <> any any (msg: "SEQ TEST"; dsize:100<>300;  sid: 100001; rev:1;)** |
| Sameip | Filtering the source and destination IP addresses for duplication. **alert ip any any <> any any (msg: "SAME-IP TEST";  sameip; sid: 100001; rev:1;)** |

Remember, once you create a rule, it is a local rule and should be in your "local.rules" file. This file is located under "/etc/snort/rules/local.rules". A quick reminder on how to edit your local rules is shown below.

![image](https://user-images.githubusercontent.com/80647611/214551612-ac0c6288-c538-475b-9c66-a84be7e77ddd.png)

That is your "local.rules" file.
![image](https://user-images.githubusercontent.com/80647611/214551666-276182be-c41a-4286-bf34-3f26f110a84b.png)

Note that there are some default rules activated with snort instance. These rules are deactivated to manage your rules and improve your exercise experience. For further information, please refer to the TASK-10 or [Snort manual](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/).

By this point, we covered the primary structure of the Snort rules. Understanding and practicing the fundamentals is suggested before creating advanced rules and using additional options.

Wow! We have covered the fundamentals of the Snort rules!
