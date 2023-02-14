# Zeek Signatures

Zeek supports signatures to have rules and event correlations to find noteworthy activities on the network. Zeek signatures use low-level pattern matching and cover conditions similar to Snort rules. Unlike Snort rules, Zeek rules are not the primary event detection point. Zeek has a scripting language and can chain multiple events to find an event of interest. We focus on the signatures in this task, and then we will focus on Zeek scripting in the following tasks.

Zeek signatures are composed of three logical paths; signature id, conditions and action. The signature breakdown is shown in the table below;

| **Signature id** | **Unique** signature name |
| ------------ | ------------------ |
| **Conditions** | **Header:** Filtering the packet headers for specific source and destination addresses, protocol and port numbers. **Content:** Filtering the packet payload for specific value/pattern. |
| **Action** | **Default action:** Create the "signatures.log" file in case of a signature match. Additional action: Trigger a Zeek script. |

Now let's dig more into the Zeek signatures. The below table provides the most common conditions and filters for the Zeek signatures.

| Condition Field |	Available Filters |
| -------------- | ---------------- |
| Header	| **src-ip:** Source IP. dst-ip: Destination IP. src-port: Source port. dst-port: Destination port. ip-proto: Target protocol. Supported protocols; TCP, UDP, ICMP, ICMP6, IP, IP6 |
| Content	| **payload:** Packet payload. http-request: Decoded HTTP requests. http-request-header: Client-side HTTP headers. http-request-body: Client-side HTTP request bodys. http-reply-header: Server-side HTTP headers. http-reply-body: Server-side HTTP request bodys. ftp: Command line input of FTP sessions. |
| Context	| **same-ip:** Filtering the source and destination addresses for duplication. |
| Action	| **event:** Signature match message. |
| Comparison Operators	| ==, !=, <, <=, >, >= |
| NOTE!	 | Filters accept string, numeric and regex values. |

![image](https://user-images.githubusercontent.com/80647611/218677941-d668de4e-50d7-4a58-92b3-4e9bd973097e.png)

## Example | Cleartext Submission of Password
Let's create a simple signature to detect HTTP cleartext passwords.
```shell 
signature http-password {
     ip-proto == tcp
     dst_port == 80
     payload /.*password.*/
     event "Cleartext Password Found!"
}

# signature: Signature name.
# ip-proto: Filtering TCP connection.
# dst-port: Filtering destination port 80.
# payload: Filtering the "password" phrase.
# event: Signature match message.
```
Remember, Zeek signatures support regex. Regex ".*" matches any character zero or more times. The rule will match when a "password" phrase is detected in the packet payload. Once the match occurs, Zeek will generate an alert and create additional log files (signatures.log and notice.log).

## Example | FTP Brute-force

Let's create another rule to filter FTP traffic. This time, we will use the FTP content filter to investigate command-line inputs of the FTP traffic. The aim is to detect FTP "admin" login attempts. This basic signature will help us identify the admin login attempts and have an idea of possible admin account abuse or compromise events.
```shell
signature ftp-admin {
     ip-proto == tcp
     ftp /.*USER.*dmin.*/
     event "FTP Admin Login Attempt!"
}
```

### Let's optimise our rule and make it detect all possible FTP brute-force attempts.

This signature will create logs for each event containing "FTP 530 response", which allows us to track the login failure events regardless of username. 
```shell
signature ftp-brute {
     ip-proto == tcp
     payload /.*530.*Login.*incorrect.*/
     event "FTP Brute-force Attempt"
}
```

Zeek signature files can consist of multiple signatures. Therefore we can have one file for each protocol/situation/threat type. Let's demonstrate this feature in our global rule.

```shell
signature ftp-username {
    ip-proto == tcp
    ftp /.*USER.*/
    event "FTP Username Input Found!"
}

signature ftp-brute {
    ip-proto == tcp
     payload /.*530.*Login.*incorrect.*/
    event "FTP Brute-force Attempt!"
}
```
