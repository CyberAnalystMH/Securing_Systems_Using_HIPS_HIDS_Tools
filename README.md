WORK IN PROGRESS
# Securing Systems using, Suricata, Snort, Fail2Ban and UFW (HIPS & HIDS) 
Summary
---
One of the things I like in the Cybersecurity world is the different tools and solutions that are out there, which many of them are open-source and don't cost a penny. Nothing wrong with tools costing money but tools like Suricata, Snort, Fail2ban and UFW allows learning at little to no cost. I was initially going to turn this GitHub project into a series, but that's maybe too many repos. In terms of IDS/IPS, I usually go with Wazuh, it's easy to use and fun but I want to expand my knowledge of IDS/IPS tools. 

Setup
---
**Rules & Objectives:**
- Secure the machines (We're going to use **4 Linux Servers, running Rocky Linux (SELinux is disabled**)
- Understand mentioned tools better
- Write and configure Rules
- Ensure it's working
- FTP (21) and SSH (22) is on and enabled as an attack surface
- Pen-Test the Servers using Kali Linux to simulate an attacker
- Have fun
  
**Why 4 Linux Servers:** Due to all the tools mentioned, being IPS/IDS, they can easily conflict with each other and cause a lot of false alerts (Negative or Positive).
  
Suricata (Only IDS) 
---
**What is it:** Suricata is a Intrusion Detection System and a Intrusion Prevention System or IDS/IPS for short, it's more CLI driven but faster then some tools like Wazuh, where it's mainly GUI driven. For this project purpose, we're going to only set-up Suricata as an IDS

**On Server1:** 

<img width="471" height="25" alt="image" src="https://github.com/user-attachments/assets/43c7eee6-55af-4a2c-9360-c969ed45d9e0" />

**Annotations:** Installing Suricata isn't as straight forward in Rocky as it is in some other Linux disros like Ubuntu Server. First, I had to install dnf-command(copr) then dnf copr enable @oisf/suricata-latest and then wrote what the screenshot shows. 


<img width="610" height="45" alt="image" src="https://github.com/user-attachments/assets/5396f9ce-64ac-4aca-a3c7-9ebeb8455159" />

**Annotations:** I simply configured the IP and network card on the yaml and then ran suricata-update to update my configs. 

<img width="696" height="51" alt="image" src="https://github.com/user-attachments/assets/3de3fc9f-065a-4455-ad3e-0a48293c4068" />


**Annotations:** For now, we're gonna use pre-existing rules for a quick test run, after enabling the source, we update suricata again.


**Then:**

<img width="800" height="32" alt="image" src="https://github.com/user-attachments/assets/e1ed9c0b-062e-475a-b4ea-ea5eab0b4733" />


**Annotations:** For a quick test.

**Writing a very simple rule and testing it:**
<img width="1121" height="55" alt="image" src="https://github.com/user-attachments/assets/9533ca78-ef5c-4863-b88d-627191966eab" />
<img width="1150" height="37" alt="image" src="https://github.com/user-attachments/assets/42440a13-1ea7-4a3d-8f02-44f4e738c8e8" />


**Annotations:** This rule detects any incoming pings on any port, the syntax is simple. However, to speed our workflow, their is a website that helps with rule writing known as "Snorpy 2.0"

**Example of Rule on Snorpy 2.0:** 
<img width="873" height="490" alt="image" src="https://github.com/user-attachments/assets/e8bee790-706e-41c9-a4fc-7d2740ae1f4c" />

**Annotations:** This website can help users write more complex syntax for specific rules.  

**Testing Pre-Made Rules**

<img width="1016" height="17" alt="image" src="https://github.com/user-attachments/assets/41d68235-43a2-4526-878b-2fdac2f16f60" />


**Annotations:** There's a lot of Pre-Made rules that also help with the IDS/IPS detection and setup. 


Snort  (Only IDS) 
---
**What is it:** Snort is also an IDS/IPS, both Suricata and Snort are pretty similar in nature and serve the same purpose, many companies use either or, or even both (Usually, not at the same time). For this project purpose, we're going to only set-up Snort as an IDS

**On Server2:** 

<img width="760" height="17" alt="image" src="https://github.com/user-attachments/assets/87aa03f9-b199-4968-8034-a31947fc3f84" />


**Annotations:** On Ubuntu server, installed and then changed the subnet on snort.conf to the appropriate subnet, then ran the second command on the screenshot to test it with the specified interface.


<img width="697" height="51" alt="image" src="https://github.com/user-attachments/assets/970e0fa0-e4c3-4848-aab1-37f8dfc9f1e8" />


**Pre - Made Rules Vs Custom Rules** 
---
(For Snort and Suricata)

| Pre - Made Rules     | Custom Rules                                    |
| -------------------- | ----------------------------------------------- |
| Very in-depth        | Takes time                                      |
| Time saving          | Can be simple and complex                       |
| Less errors          | More errors                                     |
| More false positives | Less false positives (depending if tuned right) |
| Not specific focused | Very specific focused                           |
| May cost money       | Free but costs experience and skills            |
| Too many logs        | Fair amount of logs (Depending on rules)        |
| Harder to tune       | Easier to tune                                  |


Fail2Ban  (Only IPS) 
---
**What is it:** Fail2Ban is mainly an IPS tool. It blocks any unwanted connections and puts them on a "banned" list, very similar to a firewall and it's actually a Host-Based Firewall. Fail2Ban is easy to use and very strict, sort of similar to SELinux. 


**On Server3:** 


UFW (IPS & IDS) 
---
**What is it:** UFW is similar to Fail2Ban (It's also an IPS and a Host-Base Firewall) but very simple to use and Uncomplicated, hence the name "Uncomplicated Firewall". It's great for home labs and even workstations as anyone can easily pick it up and configure it, it's actually my go to. 


**Server4:** 


 **Merging The Tools** 
---

| Efficient           | Inefficient      |
| ------------------- | ---------------- |
| Suricata + Fail2Ban | Fail2Ban + UFW   |
| Snort  + Fail2Ban   | Suricata + Snort |
| UFW + Snort         | Suricata + UFW   |
|                     |                  |
|                     |                  |


**Concept:** You can merge the depth of logs that snort and suricata has with the strictness of Fail2Ban, Suricata and Snort IPS aspect can be somewhat tasky to setup, awhile Fail2Ban is more simpler. However, the logs of Suricata and Snort may not correlate of what Fail2Ban sees.









