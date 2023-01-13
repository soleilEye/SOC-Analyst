## Creating Yara rules with yarGen

Typically this is what is done in the case of an incident, which is an event that affects/impacts the organization in a negative fashion.
We can manually open the file and attempt to sift through lines upon lines of code to find possible strings that can be used in our newly created Yara rule.
Let's check how many lines this particular file has. You can run the following: 
```shell
strings <file name> | wc -l.
```
If you try to go through each string, line by line manually, you should quickly realize that this can be a daunting task.

Luckily, we can use [yarGen](https://github.com/Neo23x0/yarGen) (yes, another tool created by Florian Roth).

## What is yarGen? yarGen is a generator for YARA rules.

From the README - "The main principle is the creation of yara rules from strings found in malware files while removing all strings that also appear in goodware files. Therefore yarGen includes a big goodware strings and opcode database as ZIP archives that have to be extracted before the first use."

Navigate to the yarGen directory, which is within tools. If you are running yarGen on your own system, you need to update it first by running the following command: `python3 yarGen.py --update`.

This will update the good-opcodes and good-strings DB's from the online repository. This update will take a few minutes. 

Once it has been updated successfully, you'll see the following message at the end of the output.

To use yarGen to generate a Yara rule for file, you can run the following command:

```shell
python3 yarGen.py -m /home/*user*/suspicious-files/file --excludegood -o /home/*user*/suspicious-files/file.yar
```

A brief explanation of the parameters above:

* `-m` is the path to the files you want to generate rules for
* `--excludegood` force to exclude all goodware strings (these are strings found in legitimate software and can increase false positives)
* `-o` location & name you want to output the Yara rule
If all is well, you should see the following output.

```shell
           [=] Generated 1 SIMPLE rules.
           [=] All rules written to /home/*user*/suspicious-files/file.yar
           [+] yarGen run finished
```

Generally, you would examine the Yara rule and remove any strings that you feel might generate false positives. For this exercise, we will leave the generated Yara rule as is and test to see if Yara will flag file or no. 

Note: Another tool created to assist with this is called yarAnalyzer (you guessed it - created by Florian Roth)

## Further Reading on creating Yara rules and using yarGen:

* https://www.bsk-consulting.de/2015/02/16/write-simple-sound-yara-rules/
* https://www.bsk-consulting.de/2015/10/17/how-to-write-simple-but-sound-yara-rules-part-2/
* https://www.bsk-consulting.de/2016/04/15/how-to-write-simple-but-sound-yara-rules-part-3/
