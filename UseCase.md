# Ansible to troubleshoot OSPF issues

## Name
Ansible to troubleshoot OSPF issues
## SubTitle
for sub title value

# Ansible to troubleshoot OSPF issues
This simple but powerful Ansible playbook can be used to troubleshoot OSPF network problems on a variety of platforms. It does not require extensive preparatory configuration for individual host state checking and rapidly discovers the vast majority of OSPF problems. 

# Objective 
* Supports Cisco IOS/IOS-XE, IOS-XR, and NX-OS platforms.
* Used to troubleshoot OSPF network problems on a variety of platforms.
* Rapidly discovers the vast majority of OSPF problems and does not require extensive preparatory configuration for individual host state checking.
* Performs all the testing in series like lint, unit, and playbook. 

# Requirements

To use this code you will need: Set up a Linux VM as an Ansible client for testing the use case.

# Instructions 
1. Ansible is required, Version 2.6.2 is used when developing this repository.
1. Create a Python3 virtual environment.
1. Activate the virtual environment.
1. Install requirements 
     pip install -r requirements.txt
1. Run "make setup" for creating a vault password.
1. Before running the script, execute "make lint" and "make unit" commands.
1. Run "make integ" command.

## WhitePaper
forPre[WhitePaperVal](http://www.whitePaper.com/)
forPre[WhitePaperVal2](http://www.whitePaper222.com/)

## Sandbox
[Catalyst 9800 Wireless LAN Controller](https://devnetsandbox.cisco.com/RM/Diagram/Index/9900a725-c584-42ae-8d51-3ac87533c5c5?diagramType=Topology)

## LinkToLearningLab
[Networking Basics](https://developer.cisco.com/learning/modules/networking-basics/)

## SolutionOnEcosystemExchange
[Physical Density Controls](https://testing-developer.cisco.com/ecosystem/meraki/apps/5ed8fa69a0774c0a8cf97e9b/)
[Instant, custom splash pages for WiFi access](https://testing-developer.cisco.com/ecosystem/meraki/apps/5a6d16371df81231b1403a81/)
