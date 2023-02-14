# Zeek Scripts

Zeek has its own event-driven scripting language, which is as powerful as high-level languages and allows us to investigate and correlate the detected events. Since it is as capable as high-level programming languages, you will need to spend time on Zeek scripting language in order to become proficient. In this room, we will cover the basics of Zeek scripting to help you understand, modify and create basic scripts. Note that scripts can be used to apply a policy and in this case, they are called policy scripts.

| Desk | Path |
| ------------- | :------------------: |
| Zeek has base scripts installed by default, and these are not intended to be modified. | These scripts are located in  "/opt/zeek/share/zeek/base". |
| User-generated or modified scripts should be located in a specific path. | These scripts are located in "/opt/zeek/share/zeek/site". |
| Policy scripts are located in a specific path. | These scripts are located in "/opt/zeek/share/zeek/policy". |
| Like Snort, to automatically load/use a script in live sniffing mode, you must identify the script in the Zeek configuration file. | You can also use a script for a single run, just like the signatures. The configuration file is located in "/opt/zeek/share/zeek/site/local.zeek". |

* Zeek scripts use the ".zeek" extension.
* Do not modify anything under the "zeek/base" directory. User-generated and modified scripts should be in the "zeek/site" directory.
* You can call scripts in live monitoring mode by loading them with the command `load @/script/path` or `load @script-name` in local.zeek file. 
* Zeek is event-oriented, not packet-oriented! We need to use/write scripts to handle the event of interest.

Now let's see Zeek scripts in action. First, let's look at the components of the Zeek script. Here the first, second and fourth lines are the predefined syntaxes of the scripting language. The only part we created is the third line which tells Zeek to extract DHCP hostnames. Now compare this automation ease with the rest of the methods. Obviously, this four-line script is easier to create and use. While tcpdump and tshark can provide similar results, transferring uncontrolled data through multiple pipelines is not much preferred.

```shell
event dhcp_message (c: connection, is_orig: bool, msg: DHCP::Msg, options: DHCP::Options)
{
print options$host_name;
}
```

| Customized script locations |
| :----------: |
| /opt/zeek/share/zeek/base/bif |
| /opt/zeek/share/zeek/base/bif/plugins |
| /opt/zeek/share/zeek/base/protocols |
