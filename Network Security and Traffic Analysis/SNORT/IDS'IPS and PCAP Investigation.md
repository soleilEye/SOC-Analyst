![c94d825d581eaef1fdc2f9c1ba3cb681](https://user-images.githubusercontent.com/80647611/214266630-f97a7b6d-6b25-4abe-8e72-3b4f28549fe8.png)
# Snort in IDS/IPS Mode

Capabilities of Snort are not limited to sniffing and logging the traffic. IDS/IPS mode helps you manage the traffic according to user-defined rules.

Note that (N)IDS/IPS mode depends on the rules and configuration.


Let's run Snort in IDS/IPS Mode

NIDS mode parameters are explained in the table below;
| Parameter	 | Description |
| ----- | -------- |
| -c | Defining the configuration file. |
| -T | Testing the configuration file. |
| -N | Disable logging. |
| -D | Background mode. |
| -A | Alert modes **full:** Full alert mode, providing all possible information about the alert. This one also is the default mode; once you use -A and don't specify any mode, snort uses this mode. **fast:**  Fast mode shows the alert message, timestamp, source and destination IP, along with port numbers.**console:** Provides fast style alerts on the console screen. **cmg:** CMG style, basic header details with payload in hex and text format. **none:** Disabling alerting. |

Let's start using each parameter and see the difference between them. Snort needs active traffic on your interface, so we need to generate traffic to see Snort in action. To do this, use the `traffic-generator` script and sniff the traffic. 

`Once you start running IDS/IPS mode`, you need to use rules. As we mentioned earlier, we will use a pre-defined ICMP rule as an example. The defined rule will only generate alerts in any direction of ICMP packet activity.

`alert icmp any any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)`

This rule is located in `"/etc/snort/rules/local.rules".`

Remember, in this module, we will focus only on the operating modes. Snort will create an "alert" file if the traffic flow triggers an alert. One last note; once you start running IPS/IDS mode, the sniffing and logging mode will be semi-passive. However, you can activate the functions using the parameters discussed in previous tasks. (-i, -v, -d, -e, -X, -l, -K ASCII).

## IDS/IPS mode with parameter "-c and -T"

Start the Snort instance and test the configuration file. 
```shell 
sudo snort -c /etc/snort/snort.conf -T
```
This command will check your configuration file and prompt it if there is any misconfiguratioın in your current setting.

## IDS/IPS mode with parameter "-N"

Start the Snort instance and disable logging by running the following command: 
```shell 
sudo snort -c /etc/snort/snort.conf -N
```

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. This command will disable logging mode. The rest of the other functions will still be available (if activated).

The command-line output will provide the information requested with the parameters. So, if you activate verbosity `-v` or full packet dump `-X` you will still have the output in the console, but there will be no logs in the log folder.

## IDS/IPS mode with parameter "-D"

Start the Snort instance in background mode with the following command: 
```shell 
sudo snort -c /etc/snort/snort.conf -D
```

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start processing the packets and accomplish the given task with additional parameters.

The command-line output will provide the information requested with the parameters. So, if you activate verbosity `-v` or full packet dump `-X` with packet logger mode `-l` you will still have the logs in the logs folder, but there will be no output in the console.

Once you start the background mode and want to check the corresponding process, you can easily use the "ps" command as shown below 
```shell 
ps -ef | grep snort
```
If you want to stop the daemon, you can easily use the "kill" command to stop the process.
```shell
sudo kill -9 PID
```
**Note that** daemon mode is mainly used to automate the Snort. This parameter is mainly used in scripts to start the Snort service in the background. It is not recommended to use this mode unless you have a working knowledge of Snort and stable configuration.

## IDS/IPS mode with parameter "-A"

Remember that there are several alert modes available in snort;

**console:** Provides fast style alerts on the console screen.
**cmg:** Provides basic header details with payload in hex and text format.
**full:** Full alert mode, providing all possible information about the alert.
**fast:** Fast mode, shows the alert message, timestamp, source and destination ip along with port numbers.
**none:** Disabling alerting.

In this section, only the **console** and **cmg** parameters provide alert information in the console. It is impossible to identify the difference between the rest of the alert modes via terminal. Differences can be identified by looking at generated logs. 

At the end of this section, we will compare the **full**, **fast** and **none** modes. Remember that these parameters don't provide console output, so we will continue to identify the differences through log formats.

## IDS/IPS mode with parameter "-A console"

Console mode provides fast style alerts on the console screen. Start the Snort instance in **console alert mode `-A console` with the following command**
```shell 
sudo snort -c /etc/snort/snort.conf -A console
```
Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 

![Screenshot 2023-01-24 172052](https://user-images.githubusercontent.com/80647611/214319109-e5375d1d-8f70-4c83-ac66-c66577faed9c.jpg)

## IDS/IPS mode with parameter "-A cmg"

Cmg mode provides basic header details with payload in hex and text format. Start the Snort instance in cmg alert mode `-A cmg` with the following command 
```shell 
sudo snort -c /etc/snort/snort.conf -A cmg
```
Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 

![Screenshot 2023-01-24 172241](https://user-images.githubusercontent.com/80647611/214319545-d9edfa5c-f400-42e4-b9ef-42c8af859f08.jpg)

**Let's compare the console and cmg outputs** before moving on to other alarm types. As you can see in the given outputs above, console mode provides basic header and rule information. **Cmg mode** provides full packet details along with rule information. 

## IDS/IPS mode with parameter "-A fast"

Fast mode provides alert messages, timestamps, and source and destination IP addresses. **Remember, there is no console output in this mode.** Start the Snort instance in fast alert mode `-A fast` with the following command 
```shell 
sudo snort -c /etc/snort/snort.conf -A fast
```
Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 

Let's check the alarm file;
![c66d9e4fb20937682ee367346a1d0f4b](https://user-images.githubusercontent.com/80647611/214320743-3b71a947-6e8b-4a21-b12b-8f03e517ce7b.png)

As you can see in the given picture above, fast style alerts contain summary information on the action like direction and alert header.

## IDS/IPS mode with parameter "-A full"

Full alert mode provides all possible information about the alert. **Remember, there is no console output in this mode.** Start the Snort instance in full alert mode `-A full` with the following command 
```shell 
sudo snort -c /etc/snort/snort.conf -A full
```
Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 
Let's check the alarm file;
![cba862ab1b89fe31fe0ac1c356fde8fa](https://user-images.githubusercontent.com/80647611/214321300-52566a13-7dd0-4a8c-9129-6e76fb988ec7.png)

As you can see in the given picture above, full style alerts contain all possible information on the action.

## IDS/IPS mode with parameter "-A none"

Disable alerting. This mode doesn't create the alert file. However, it still logs the traffic and creates a log file in binary dump format. **Remember, there is no console output in this mode.** Start the Snort instance in none alert mode `-A none` with the following command 
```shell 
sudo snort -c /etc/snort/snort.conf -A none
```
Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 

## IDS/IPS mode: "Using rule file without configuration file"
It is possible to run the Snort only with rules without a configuration file. Running the Snort in this mode will help you test the user-created rules. However, this mode will provide less performance.

## IPS mode and dropping packets
Snort IPS mode activated with **-Q --daq afpacket** parameters. You can also activate this mode by editing snort.conf file. However, you don't need to edit snort.conf file in the scope of this room. Review the bonus task or snort manual for further information on daq and advanced configuration settings: `-Q --daq afpacket`

Activate the Data Acquisition (DAQ) modules and use the afpacket module to use snort as an IPS: `-i eth0:eth1`
Identifying interfaces note that Snort IPS require at least two interfaces to work. Now run the traffic-generator script as sudo and start ICMP/HTTP traffic.

As you can see in the picture above, Snort blocked the packets this time. **We used the same rule with a different action (drop/reject).** Remember, for the scope of this task; our point is the operating mode, not the rule.

# Operation Mode 4: PCAP Investigation
![cd4c3186f99950f6896a9c00007d0001](https://user-images.githubusercontent.com/80647611/214532667-07fe102f-f39b-4996-888e-3a573625af60.png)

## Let's investigate PCAPs with Snort

Capabilities of Snort are not limited to sniffing, logging and detecting/preventing the threats. PCAP read/investigate mode helps you work with pcap files. Once you have a pcap file and process it with Snort, you will receive default traffic statistics with alerts depending on your ruleset.

Reading a pcap without using any additional parameters we discussed before will only overview the packets and provide statistics about the file. In most cases, this is not very handy. We are investigating the pcap with Snort to benefit from the rules and speed up our investigation process by using the known patterns of threats. 

Note that we are pretty close to starting to create rules. Therefore, you need to grasp the working mechanism of the Snort, learn the discussed parameters and begin combining the parameters for different purposes.

PCAP mode parameters are explained in the table below;
| Parameter	 | Description |
| ----- | -------- |
| -r / --pcap-single= | Read a single pcap |
| --pcap-list=""| Read pcaps provided in command (space separated). |
| --pcap-show | Show pcap name on console during processing.|

## Investigating single PCAP with parameter "-r"

For test purposes, you can still test the default reading option with pcap by using the following command 
```shell 
snort -r icmp-test.pcap
```
Let's investigate the pcap with our configuration file and see what will happen. 
```shell 
sudo snort -c /etc/snort/snort.conf -q -r icmp-test.pcap -A console -n 10
```
![image](https://user-images.githubusercontent.com/80647611/214533752-d57c4bfd-8f2a-48aa-a720-42dba374e814.png)

Our ICMP rule got a hit! As you can see in the given output, snort identified the traffic and prompted the alerts according to our ruleset.

## Investigating multiple PCAPs with parameter "--pcap-list"

Let's investigate multiple pcaps with our configuration file and see what will happen. 
```shell 
sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console -n 10
```
Our ICMP rule got a hit! As you can see in the given output, snort identified the traffic and prompted the alerts according to our ruleset.

**Here is one point to notice:** we've processed two pcaps, and there are lots of alerts, so it is impossible to match the alerts with provided pcaps without snort's help. We need to separate the pcap process to identify the source of the alerts.

## Investigating multiple PCAPs with parameter "--pcap-show"
Let's investigate multiple pcaps, distinguish each one, and see what will happen. 
```shell 
sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console --pcap-show
```
![image](https://user-images.githubusercontent.com/80647611/214535806-c46f7c33-0f2f-43a8-b619-10e91b0c5132.png)
Our ICMP rule got a hit! As you can see in the given output, snort identified the traffic, distinguished each pcap file and prompted the alerts according to our ruleset.
