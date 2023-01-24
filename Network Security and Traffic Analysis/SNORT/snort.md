# The First Interaction with Snort

[tgn](https://manpages.ubuntu.com/manpages/trusty/man1/tgn.1.html) - a network traffic generator 
First, let's verify snort is installed. The following command will show you the instance version.

```shell
snort -V
```

Before getting your hands dirty, we should ensure our configuration file is valid.
```shell
sudo snort -c /etc/snort/snort.conf -T 
```

Here `"-T"` is used for testing configuration, and `"-c"` is identifying the configuration file (snort.conf). Note that it is possible to use an additional configuration file by pointing it with "-c". 

```shell 
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -T 

        --== Initializing Snort ==--
Initializing Output Plugins!
Initializing Preprocessors!
Initializing Plug-ins!
... [Output truncated]
        --== Initialization Complete ==--

   ,,_     -*> Snort! <*-
  o"  )~   Version 2.9.7.0 GRE (Build XXXX) 
   ''''    By Martin Roesch & The Snort Team: http://www.snort.org/contact#team
           Copyright (C) 2014 Cisco and/or its affiliates. All rights reserved.
           Copyright (C) 1998-2013 Sourcefire, Inc., et al.
           Using libpcap version 1.9.1 (with TPACKET_V3)
           Using PCRE version: 8.39 2016-06-14
           Using ZLIB version: 1.2.11

           Rules Engine: SF_SNORT_DETECTION_ENGINE  Version 2.4  
           Preprocessor Object: SF_GTP  Version 1.1  
           Preprocessor Object: SF_SIP  Version 1.1  
           Preprocessor Object: SF_SSH  Version 1.1  
           Preprocessor Object: SF_SMTP  Version 1.1  
           Preprocessor Object: SF_POP  Version 1.0  
           Preprocessor Object: SF_DCERPC2  Version 1.0  
           Preprocessor Object: SF_IMAP  Version 1.0  
           Preprocessor Object: SF_DNP3  Version 1.1  
           Preprocessor Object: SF_SSLPP  Version 1.1  
           Preprocessor Object: SF_MODBUS  Version 1.1  
           Preprocessor Object: SF_SDF  Version 1.1  
           Preprocessor Object: SF_REPUTATION  Version 1.1  
           Preprocessor Object: SF_DNS  Version 1.1  
           Preprocessor Object: SF_FTPTELNET  Version 1.2  
... [Output truncated]
Snort successfully validated the configuration!
Snort exiting
```

Once we use a configuration file, snort got much more power! The configuration file is an all-in-one management file of the snort. Rules, plugins, detection mechanisms, default actions and output settings are identified here. It is possible to have multiple configuration files for different purposes and cases but can only use one at runtime.

Note that every time you start the Snort, it will automatically show the default banner and initial information about your setup. You can prevent this by using the `"-q"` parameter.
| Parametr | Description |
| -------------|----------|
| -V / --version | This parameter provides information about your instance version. |
| -c | Identifying the configuration file |
| -T | Snort's self-test parameter, you can test your setup with this parameter. |
| -q | 	Quiet mode prevents snort from displaying the default banner and initial information about your setup. |

# Operation Mode 1: Sniffer Mode

## Let's run Snort in Sniffer Mode

Like tcpdump, Snort has various flags capable of viewing various data about the packet it is ingesting.

Sniffer mode parameters are explained in the table below;

| Parametr | Description |
| -------------|----------|
| -v | Verbose. Display the TCP/IP output in the console. |
| -d | Display the packet data (payload). |
| -e | Display the link-layer (TCP/IP/UDP/ICMP) headers.  |
| -X | Display the full packet details in HEX. |
| -i | This parameter helps to define a specific network interface to listen/sniff. Once you have multiple interfaces, you can choose a specific interface to sniff. |

## Sniffing with parameter "-i"

Start the Snort instance in verbose mode `-v` and use the interface `-i "eth0"`; 
```shell 
sudo snort -v -i eth0
```

In case you have only one interface, Snort uses it by default. The above example demonstrates to sniff on the interface named "eth0". Once you simulate the parameter -v, you will notice it will automatically use the "eth0" interface and prompt it.

## Sniffing with parameter "-v"

Start the Snort instance in verbose mode `-v`; 
```shell
sudo snort -v
```

## Sniffing with parameter "-d"

Start the Snort instance in dumping packet data mode `-d`; 
```shell
sudo snort -d
```
## Sniffing with parameter "-de"

Start the Snort instance in dump `-d` and link-layer header grabbing `-e` mode; 
```shell
snort -d -e
```
## Sniffing with parameter "-X"

Start the Snort instance in full packet dump mode `-X`; 
```shell
sudo snort -X
```

# Operation Mode 2: Packet Logger Mode

## Let's run Snort in Logger Mode

You can use Snort as a sniffer and log the sniffed packets via logger mode. You only need to use the packet logger mode parameters, and Snort does the rest to accomplish this.

Packet logger parameters are explained in the table below;

| Parameter | Description |
| ------------- | ---------------- |
| -l | Logger mode, target **log and alert** output directory. Default output folder is /var/log/snort. The default action is to dump as tcpdump format in **/var/log/snort** |
| -K ASCII | Log packets in ASCII format. |
| -r | Reading option, read the dumped logs in Snort. |
| -n | Specify the number of packets that will process/read. Snort will stop after reading the specified number of packets. |

Let's start using each parameter and see the difference between them. Snort needs active traffic on your interface, so we need to generate traffic to see Snort in action.

## Logfile Ownership
Before generating logs and investigating them, we must remember the Linux file ownership and permissions. No need to deep dive into user types and permissions. The fundamental file ownership rule; **whoever creates a file becomes the owner of the corresponding file.**

Snort needs superuser (root) rights to sniff the traffic, so once you run the snort with the "sudo" command, the "root" account will own the generated log files. Therefore you will need "root" rights to investigate the log files. There are two different approaches to investigate the generated log files;

* **Elevation of privileges** - You can elevate your privileges to examine the files. You can use the "sudo" command to execute your command as a superuser with the following command `sudo command`. You can also elevate the session privileges and switch to the superuser account to examine the generated log files with the following command: `sudo su`
* **Changing the ownership of files/directories** - You can also change the ownership of the file/folder to read it as your user: `sudo chown username file` or `sudo chown username -R directory` The `-R` parameter helps recursively process the files and directories.

## Logging with parameter "-l"

First, start the Snort instance in packet logger mode; 
```shell
sudo snort -dev -l .
```

Now start ICMP/HTTP traffic with the traffic-generator script.

Once the traffic is generated, Snort will start showing the packets and log them in the target directory. You can configure the default output directory in snort.config file. However, you can use the `-l` parameter to set a target directory. Identifying the default log directory is useful for continuous monitoring operations, and the `-l` parameter is much more useful for testing purposes.

The `-l`. part of the command creates the logs in the current directory. You will need to use this option to have the logs for each exercise in their folder.

Now, let's check the generated log file.

As you can see, it is a single all-in-one log file. It is a binary/tcpdump format log.

## Logging with parameter "-K ASCII"

Start the Snort instance in packet logger mode; 
```shell 
sudo snort -dev -K ASCII -l .
```
Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, Snort will start showing the  packets in verbosity mode as follows;

The logs created with "-K ASCII" parameter is entirely different. 
Once we look closer at the created folders, we can see that the logs are in ASCII and categorised format, so it is possible to read them without using a Snort instance.
![Screenshot 2023-01-24 125156](https://user-images.githubusercontent.com/80647611/214260975-ad159953-8db4-4975-8157-8fe16e33f332.jpg)

In a nutshell, ASCII mode provides multiple files in human-readable format, so it is possible to read the logs easily by using a text editor. By contrast with ASCII format, binary format is not human-readable and requires analysis using Snort or an application like tcpdump.

Let's compare the ASCII format with the binary format by opening both of them in a text editor. The difference between the binary log file and the ASCII log file is shown below. (Left side: binary format. Right side: ASCII format).![5e8487745a7ee4d3d33e67c2967ebaba](https://user-images.githubusercontent.com/80647611/214259951-1666eaa6-df8f-4d73-b39b-23409a4bf486.png)

## Reading generated logs with parameter "-r"
Start the Snort instance in packet reader mode; 
```shell 
sudo snort -r
```
**Note that** Snort can read and handle the binary like output (tcpdump and Wireshark also can handle this log format). However, if you create logs with "-K ASCII" parameter, Snort will not read them. As you can see in the above output, Snort read and displayed the log file just like in the sniffer mode.

Opening log file with tcpdump.
![Screenshot 2023-01-24 125542](https://user-images.githubusercontent.com/80647611/214261763-68bd1c51-0787-4ba8-99c3-e07dd02f5095.jpg)

Opening log file with Wireshark.
![a4bd8447760481cd2f6f9762a9620a50](https://user-images.githubusercontent.com/80647611/214261825-b5ac4870-1d4a-453f-9e7a-99caff72cc0c.png)

**`-r` parameter also allows users to filter the binary log files. You can filter the processed log to see specific packets with the `-r` parameter and Berkeley Packet Filters (BPF).**

* **sudo snort -r logname.log -X**
* **sudo snort -r logname.log icmp**
* **sudo snort -r logname.log tcp**
* **sudo snort -r logname.log 'udp and port 53'**

The output will be the same as the above, but only packets with the chosen protocol will be shown. Additionally, you can specify the number of processes with the parameter `-n`. The following command will process only **the first 10 packets**:
```shell
snort -dvr logname.log -n 10
```
Please use the following resources to understand how the BPF works and its use.
* https://en.wikipedia.org/wiki/Berkeley_Packet_Filter
* https://biot.com/capstats/bpf.html
* https://www.tcpdump.org/manpages/tcpdump.1.html
