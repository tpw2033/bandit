## Lab 5 : CEG 3400

### Intrusion Detection

Table of contents:
* [Background](LAB5-INSTRUCTIONS.md#background)
* [Objectives](LAB5-INSTRUCTIONS.md#objectives)
* [Preparation](LAB5-INSTRUCTIONS.md#preparation)
* [Task 1: Snort ICMP](LAB5-INSTRUCTIONS.md#task-1-snort-icmp)
* [Task 2: Custom Rules](LAB5-INSTRUCTIONS.md#task-2-custom-rules)
* [Task 3: Extra Credit](LAB5-INSTRUCTIONS.md#task-3-ec)

---

#### Background and Objectives

In this lab you will learn about an open source network Intrusion Detection System (IDS)
named Snort.

This lab assumes you have a basic understanding of networking, IP addresses, ports
and packets (from CEG-2350 and what was covered in class).

Students should become familiar with the following:

* Using Snort to detect ICMP ping requests
* Writing custom snort rules
* Testing custom rules

---

#### Rubrik

| Item | # Points|
| --- | --- |
| 10 commits | 10 |
| Good markdown style | 20 |
| Task 1 | 30 |
| Task 2 | 30 | 
| Task 3 | 30 BONUS |

---

#### Preparation

This lab will require all work be done in AWS.  Please deploy the below instance and work inside the lab.

* [CEG 3400 Lab 5 AWS link](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=ceg3400Lab&templateURL=https:%2F%2Fwsu-cecs-cf-templates.s3.us-east-2.amazonaws.com%2Fcourse-templates%2Fceg3400-mek.yml)
* Identify the IP address of the running EC2 instance created [in the EC2
  page](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#Instances:)
* Install `snort` with the following commands:

```bash
sudo apt update
sudo apt install snort
sudo service snort start
sudo service snort status
```

---

## Task 1: Snort ICMP

Your company is under attack by an adversary that appears to be using ping to detect live 
IP addresses on your network.  To combat this you have setup the an AWS instance (the ceg 3400 lab isntance) as a 
[honeypot](https://en.wikipedia.org/wiki/Honeypot_(computing)) in order to capture this and 
follow-up attacks for study.

After every successful ping query a few days goes by and 
that system is then infected.  You know that the `ping` itself is not the carrying any 
malicious code but you would still like to log all incoming ICMP ping requests
so you have a list of IP addresses that might be targeting your systems.

[Read up on snort](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/node27.html) (sections 3.1, 3.2, and 3.3).

Add the following to `/etc/snort/rules/local.rules` and restart the snort service.

```bash
alert icmp any any -> any any (msg:"ICMP Packet found"; sid:1000001; rev:1;)
```

To restart snort: `sudo service snort restart`

Test your new rule is logging information by pinging it from your home or other remote 
system and check the logs in `/var/log/snort/snort.log`.

NOTE: Snort logs are binary and need to be read with a special program `u2spewfoo` like so:

```bash
sudo u2spewfoo /var/log/snort/snort.log
```

Answer all questions in `README.md`.

---

## Task 2: Custom rules

Great work, your ICMP logging identified an IP address realted to these attacks!  
After some further digging you determined that sometime after the attacker pings 
your system, the victim IP makes a request out to one of 3 domains:

* www.gizoogle.net
* www.lingscars.com
* twitter.com

Create an alert to capture ***BOTH*** outgoing and incoming traffic from these three
domains to your system.  You may need to read further into the snort rule writing guide 
(section 3.5) or do some cursory google searching.

Test your rules (hint: use `curl` and dont forget to restart `snort`)

Answer all questions in `README.md`.

---

## Task 3: EC (30 Bonus points)

Choose any SINGLE rule out of `/etc/snort/rules/` (excluding `local.rules`) and do a deep dive on it.
IMPORTANT, each file in the above directory contains multiple rules.  The task is to identify a single 
rule in one of the files and describe it, NOT to describe an entire file...

Explain all parts of the rule and what they do including:
* Rule headers including IP, protocol, port, and direction
* Active rules and options including content, offset, and all relevent options to make the rule work
* Your words on what the rule is trying to detect.

Be verbose and write with good markdown style or risk not getting credit for this!

