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
