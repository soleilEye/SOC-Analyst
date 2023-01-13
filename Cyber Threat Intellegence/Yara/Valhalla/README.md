## Valhalla

**Valhalla** is an online Yara feed created and hosted by [Nextron-Systems]https://www.nextron-systems.com/valhalla/)erm, Florian Roth).

Per the website, *"Valhalla boosts your detection capabilities with the power of thousands of hand-crafted high-quality YARA rules."*

<p align="center">
  <img src="https://github.com/AM1RKA/SOC-Analyst/blob/main/Cyber%20Threat%20Intellegence/Yara/Valhalla/Valhalla.png">
</p>

From the image above, we should denote that we can conduct searches based on a keyword, tag, ATT&CK technique, sha256, or rule name. 

Taking a look at the data provided to us, let's examine the rule in the screenshot below:

<p align="center">
  <img src="https://github.com/AM1RKA/SOC-Analyst/blob/main/Cyber%20Threat%20Intellegence/Yara/Valhalla/ValhallaRules.png">
</p>

We are provided with the name of the rule, a brief description, a reference link for more information about the rule, along with the rule date. 

Picking up from our scenario, at this point, you know that the files are related. Even though Loki classified the files are suspicious, you know in your gut that they are malicious. Hence the reason you created a Yara rule using yarGen to detect it on other web servers. But let's further pretend that you are not code-savvy (FYI - not all security professionals know how to code/script or read it). You need to conduct further research regarding these files to receive approval to eradicate these files from the network. 
