---
title: "Server Upgrade - Part 1: Moving AD, DNS, and DHCP from Server 2008 to Server 2022"
categories: 
  - Windows Server
tags:
  - Windows Server 2008
  - Windows Server 2022
  - Windows Server
  - Server Upgrades
  - Active Directory
  - DHCP
  - DNS
toc: true
toc_label: "Contents"
---

2023 is the year of server upgrades for me. I have around 14 servers that all need OS upgrades, mainly from 2012 R2 to 2022, but one of the most difficult ones is the 2008 Windows Server that this post is about. Yes you heard correctly we stil have 2008 Servers in production.

## Purpose of the project

Now the 2008 server has the following roles: Active Directory (AD), DNS, DHCP, and the main company File Server, which of course is neither good or ideal. So the purpose of this project is to split the server, which is a physical server, into two new 2022 virtual servers. One server will run AD, DNS, and DHCP, and the other will be the new file server. So the project will be split into two parts:

* Part 1: Move the AD, DNS, and DHCP roles onto a new 2022 server.
* Part 2: Move the file server onto a new 2022 server, separate from the new Domain Controller (DC) server.

This server has been in production for many many years, since before I started at the company, so now I have finally got the chance to sort this mess of a server out!

## Plan of Action

For the first part of the project I made the following plan:

* Create new 2022 DC.
* Install DHCP Role on the new DC.
* Export DHCP from 2008 DC and import onto 2022 DC.
* Deauthorise 2008 DHCP server and Authorise the new 2022 DHCP server.
* Install AD on 2022 using 2008 as the template, and promote as DC.
* Transfer all DC FSMO roles from 2008 to 2022.
* Decommission 2008 DC and upgrade Domain Schema and Forest to Windows2016 version.
* Take IP address from 2008 server and assign to 2022 server to ensure static IP configs see the new 2022 server for DNS and DHCP.
* Continue to use 2008 server as file serve until part 2 of the project is complete.

## Implementing the plan

### Creating the new 2022 DC

The new 2022 DC (DC01) was created in Hyper-V and was assigned 2 vCPUs and 4GB of RAM, this seemed to be the ideal config for this server. I added the server to the domain and ensured all updates and our AV were installed.

### Install DCHP Role on 2022 DC



## Conclusion

In conclusion, make sure you constantly keep up to date with Microsoft changes, and ensure you prepare properly for them…like I should have! and also make sure you check out [the Sysadmin subreddit](https://www.reddit.com/r/sysadmin) if you are working in IT, you get some great advice on there and good banter too!

Thank you for reading!

## References

1. [https://learn.microsoft.com/en-us/microsoft-365/admin/security-and-compliance/enable-modern-authentication?view=o365-worldwide](https://www.learn.microsoft.com/en-us/microsoft-365/admin/security-and-compliance/enable-modern-authentication?view=o365-worldwide)
2. [https://techcommunity.microsoft.com/t5/exchange-team-blog/microsoft-and-apple-working-together-to-improve-exchange-online/ba-p/3513846](https://techcommunity.microsoft.com/t5/exchange-team-blog/microsoft-and-apple-working-together-to-improve-exchange-online/ba-p/3513846)
3. [https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/deprecation-of-basic-authentication-exchange-online](https://www.learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/deprecation-of-basic-authentication-exchange-online)
