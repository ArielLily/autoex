Secure SD-WAN
==============

## Tag
[stage] - Walk, Run
[LifeCycle] - Day 0, Day 1
[Domain] - Campus/Branch

The Cisco SD-WAN software provides a REST API, which is a programmatic interface for controlling, configuring, and monitoring the Cisco SD-WAN devices in an overlay network. You access the REST API through the vManage web server. This sample code uses Go to interact with the SD-WAN REST API. This should be used with [SD-WAN Release 16.9.x and Cisco SD-WAN Release 18.3.x](https://www.cisco.com/c/en/us/td/docs/routers/sdwan/release/notes/xe-16-9-18-3/sd-wan-rel-notes-16-9-18-3.html)

## Objectives

* Use the Cisco SD-WAN REST API to configure, control, and monitor SD-WAN devices in an overlay network.
* Use the authentication processes on different versions of the SD-WAN API.
* Establish HTTPS session to the server with a cookie example. When you use a program or script to transfer data from a vManage web server or 
  perform operations on the server, you must first create the session to get a cookie.
* Perform the login operation and security checks on the vManage web server at the specified IP address, so that you can use the POST method to 
  perform WAN setup and configuration.


**API authentication Process**

- Send POST request for authentication with vManage web server.
- Method: POST
- Request URL: ` https://vmanage-ip:vmanage/j_security_check`
- POST Request Payload: `{'j_username' : username, 'j_password' : password}`

**Getting/Printing Device Information**

- Method: GET
- Request URL: `https://vmanage-ip:vmanage/dataservice/device`

**Requirements**

To use this application you will need:

- Go version go1.11+
- Cisco SD-WAN 18+
- A Cisco SD-WAN account with permissions to attach and detach templates

 <img src="https://d1wqs00nbeeox1.cloudfront.net/staging/smartsheet/rc-upload-1593427827859-3/1593428426231.png" />
 
 
## Whitepaper
forPre[WhitePaperVal](http://www.whitePaper.com/)

forPre[WhitePaperVal2](http://www.whitePaper222.com/)

## Related Sandbox
[Catalyst 9800 Wireless LAN Controller](https://devnetsandbox.cisco.com/RM/Diagram/Index/9900a725-c584-42ae-8d51-3ac87533c5c5?diagramType=Topology)

## Related LearningLab
[Networking Basics](https://developer.cisco.com/learning/modules/networking-basics/)

## Solutions on EcosystemExchange
[Physical Density Controls](https://testing-developer.cisco.com/ecosystem/meraki/apps/5ed8fa69a0774c0a8cf97e9b/)

[Instant, custom splash pages for WiFi access](https://testing-developer.cisco.com/ecosystem/meraki/apps/5a6d16371df81231b1403a81/)
