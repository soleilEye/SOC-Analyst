# Scripts 101 | Write Basic Scripts

Scripts contain operators, types, attributes, declarations and statements, and directives. Let's look at a simple example event called "zeek_init" and "zeek_done". These events work once the Zeek process starts and stops. Note that these events don't have parameters, and some events will require parameters.

```shell
event zeek_init()
    {
     print ("Started Zeek!");
    }
event zeek_done()
    {
    print ("Stopped Zeek!");
    }

# zeek_init: Do actions once Zeek starts its process.
# zeek_done: Do activities once Zeek finishes its process.
# print: Prompt a message on the terminal.
```

Let's print the packet data to the terminal and see the raw data. In this script, we are requesting details of a connection and extracting them without any filtering or sorting of the data. To accomplish this, we are using the "new_connection" event. This event is automatically generated for each new connection. This script provides bulk information on the terminal. We need to get familiar with Zeek's data structure to reduce the amount of information and focus on the event of interest. To do so, we need to investigate the bulk data.

```shell
event new_connection(c: connection)
{
	print c;
}
```

To filter the event of interest, we will use the primary tag (in this case, it is c --comes from "c: connection"--), id value (id=), and field name. You should notice that the fields are the same as the fields in the log files.

```shell
event new_connection(c: connection)
{
	print ("###########################################################");
	print ("");
	print ("New Connection Found!");
	print ("");
	print fmt ("Source Host: %s # %s --->", c$id$orig_h, c$id$orig_p);
	print fmt ("Destination Host: resp: %s # %s <---", c$id$resp_h, c$id$resp_p);
	print ("");
}

# %s: Identifies string output for the source.
# c$id: Source reference field for the identifier.
```

Now you have a general idea of running a script and following the provided output on the console. Let's look closer to another script that extracts specific information from packets. The script above creates logs and prompts each source and destination address for each connection. 

# Scripts 201 | Use Scripts and Signatures Together

Up to here, we covered the basics of Zeek scripts. Now it is time to use scripts collaboratively with other scripts and signatures to get one step closer to event correlation. Zeek scripts can refer to signatures and other Zeek scripts as well. This flexibility provides a massive advantage in event correlation.

Let's demonstrate this concept with an example. We will create a script that detects if our previously created "ftp-admin" rule has a hit. 

```shell
event signature_match (state: signature_state, msg: string, data: string)
{
if (state$sig_id == "ftp-admin")
    {
    print ("Signature hit! --> #FTP-Admin ");
    }
}
```

This basic script quickly checks if there is a signature hit and provides terminal output to notify us. We are using the "signature_match" event to accomplish this. You can read more about events [here](https://docs.zeek.org/en/master/scripts/base/bif/event.bif.zeek.html?highlight=signature_match). Note that we are looking only for "ftp-admin" signature hits. The signature is shown below. 

```shell
signature ftp-admin {
    ip-proto == tcp
    ftp /.*USER.*admin.*/
    event "FTP Username Input Found!"
}
```

## Scripts 202 | Load Local Scripts

### Load all local scripts

We mentioned that Zeek has base scripts located in "/opt/zeek/share/zeek/base". You can load all local scripts identified in your "local.zeek" file. Note that base scripts cover multiple framework functionalities. You can load all base scripts by easily running the `local` command.

```shell
zeek -C -r ftp.pcap local 
```

# Scripts 203 | Load Frameworks

Zeek has 15+ frameworks that help analysts to discover the different events of interest. In this task, we will cover the common frameworks and functions. You can find and read more on the prebuilt scripts and frameworks by visiting Zeek's online book here.

### File Framework | Hashes

Not all framework functionalities are intended to be used in CLI mode. The majority of them are used in scripting. You can easily see the usage of frameworks in scripts by calling a specific framework as `load @ $PATH/base/frameworks/framework-name`. Now, let's use a prebuilt function of the file framework and have MD5, SHA1 and SHA256 hashes of the detected files. We will call the "File Analysis" framework's "hash-all-files" script to accomplish this. Before loading the scripts, let's look at how it works.

![image](https://user-images.githubusercontent.com/80647611/218695370-1aa6baf5-8605-46ad-8538-a7c0f398184c.png)

### Notice Framework | Intelligence

The intelligence framework can work with data feeds to process and correlate events and identify anomalies. The intelligence framework requires a feed to match and create alerts from the network traffic. Let's demonstrate a single user-generated threat intel file and let Zeek use it as the primary intelligence source. 

Intelligence source location: `/opt/zeek/intel/zeek_intel.txt`

There are two critical points you should never forget. First, the source file has to be tab-delimited. Second, you can manually update the source and adding extra lines doesn't require any re-deployment. However, if you delete a line from the file, you will need to re-deploy the Zeek instance. 

Let's add the suspicious URL gathered from the case1.pcap file as a source intel and see this feature in action! Before executing the script, let's look at the intelligence file and the script contents.

# Scripts 204 | Package Manager

Zeek Package Manager helps users install third-party scripts and plugins to extend Zeek functionalities with ease. The package manager is installed with Zeek and available with the `zkg` command. Users can install, load, remove, update and create packages with the "zkg" tool. You can read more on and view available packages [here](https://packages.zeek.org/) and [here](https://github.com/zeek/packages). Please note that you need root privileges to use the "zkg" tool.

| Command | Description |
| -------- | :--------: |
zkg install package_path | Install a package. Example (zkg install zeek/j-gras/zeek-af_packet-plugin). |
zkg install git_url | Install package. Example (zkg install https://github.com/corelight/ztest). |
zkg list | List installed package. |
zkg remove | Remove installed package. |
zkg refresh | Check version updates for installed packages. |
zkg upgrade | Update installed packages. |
