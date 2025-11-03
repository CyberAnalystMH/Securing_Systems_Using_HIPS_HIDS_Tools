WORK IN PROGRESS
# Securing Systems using, Suricata, Snort, Fail2Ban and UFW (HIPS & HIDS) 

# Summary
One of the things I like in the Cybersecurity world is the different tools and solutions that are out there, which many of them are open-source and don't cost a penny. Nothing wrong with tools costing money but tools like Suricata, Snort, Fail2ban and UFW allows learning at little to no cost. I was initially going to turn this GitHub project into a series, but that's maybe too many repos. In terms of IDS/IPS, I usually go with Wazuh, it's easy to use and fun but I want to expand my knowledge of IDS/IPS tools. 

# Setup

**Rules & Objectives:**
- Secure the machines (We're going to use **4 Linux Servers, running Rocky Linux (SELinux is disabled**)
- Understand mentioned tools better
- Write and configure Rules
- Ensure it's working
- FTP (21) and SSH (22) is on and enabled as an attack surface
- Pen-Test the Servers using Kali Linux to simulate an attacker
- Have fun
**Why 4 Linux Servers:** Due to all the tools mentioned, being IPS/IDS, they can easily conflict with each other and cause a lot of false alerts (Negative or Positive).


  # Suricata
  
**What is it:** Suricata is a Intrusion Detection System and a Intrusion Prevention System or IDS/IPS for short, it's more CLI driven but faster then some tools like Wazuh, where it's mainly GUI driven. 

**On Server1:** 
