# The First Interaction with Snort

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
