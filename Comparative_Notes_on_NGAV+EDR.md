## Notes on EDR Endpoint Protection

**Conditions**

 - 100% cloud based,  with no on-prem server hardware or software
 - Moves beyond simple AV to endpoint detection and response (EDR) type capabilities
 - On the business side, they must have some kind of reseller program that we can sign up with
 - Multi-tenancy, allowing us to view all clients on one dashboard through a “single pane of glass”
 - Integration with Splunk that is capable enough for us not to have to do any monitoring of the endpoint console itself
 - Ideally, some kind of webhook/api capability so Splunk can be used to trigger actions on workstations
 - The ability to do some device management, perhaps restrict external storage/usb devices
 - They should all be sold on a per seat per month pricing structure, once you have a few contenders you’d need to reach out to them to see what that looks like.
 
Perhaps do a first pass to see if you can find any other contenders and let me know what the final list of potential options looks like, you can then start researching/testing them in more detail.
 - [NSS Labs Advanced Endpoint Protection Deep-Dive](https://www.nextgenguard.com/datasheets/NSS%20Labs_Advanced%20Endpoint%20Protection%20Comparative%20Report_Security%20Value%20Map.pdf)
 - Takeaways:
   - Carbon Black's CB Defense -  the highest cost of the proposed options with a Total Cost of Ownership (TCO) of $245, and had an above average security effectiveness of 93.6%
   - SentinelOne had a below average TCO of $148, with an above average security effectiveness of 97.7%
   - Palo Alto Traps had an above average TCO of $146, with an above average security effectiveness of 97.7%
   - Crowdstrike was not tested
   - Other noteworthy options are Trend Micro, EnSilo, and Palo Alto Networks
___

#### Use Cases

This service should integrate with Splunk SIEM and provide Anti-virus and EDR to our clients. 

There will be only one or two people managing the SIEM server and the security monitoring for the clients who choose to upgrade to the enhanced security package. For the majority of our clients, PHI or PCI data will not be a factor. While we do execute routine vulnerability management scans, we have not been audited by any network security service and OSIbeyond has not been pentested.
___

#### NGAV+EDR - State of the Industry

There are about a dozen leading providers of NGAV+EDR, with some who specialize in the field, and some, like Cisco and Microsoft, that have the option available. Every single NGAV+EDR is cloud-based, and every single one uses some from of machine learning/artificial intelligence. Most of these services actually sound fairly similar to each other in how they work and what they can do. For instance, every one of these four choices outlined in this document will boast the same methodology for endpoint detection and protection: *This cloud-based software, which is installed by agent onto an endpoint, and works online and offline, uses behavioral-analysis facilitated by AI/ML, instead of traditional signature analysis, to detect threats, viruses, and malware, and kill or quarantine the process before the action can be completed.*

Most of the information in this document was sourced from the datasheets and technical specifications of each product, and from information provided from each company's desperate salespeople. Pros and cons and other opinionative content was generated from Gartner Peer reviews and NSS Labs, as well as Reddit comments on certain subreddits like /r/sysadmin, /r/netsec, /r/asknetsec, etc. 
___

### Carbon Black's **CB Defense**

 - [Carbon Black CB Defense Datasheet](https://www.carbonblack.com/wp-content/uploads/2018/12/CB_Defense_DataSheet_122018_RGB.pdf)

Requirements, met, unmet:
 - CB Defense is entirely cloud-based
 - They do have an MSSP reseller program, which typically offers a 30%-37% discount, and reduces the minimum purchase of licenses to 50, per client
   - For MSPs, every client must be disclosed to Carbon Black, and the client must have a minimum of 50 licenses purchased for them. Any unneeded licenses will be discounted, but not free. If the MSP is not an MSSP partner, reselling has no discount and requires a minimum purchase of 100 licenses per client
 - Multi-tenancy is a flagship feature, and we would be able to create different rules for different clients from within the same CB Defense control panel, or Splunk
 - Can be integrated with Splunk (pre-built-in) or through SolarWinds, or 300 other SIEM/Monitoring tools, but can only natively allow device configuration changes through the console
 - Has an open API, and we can develop our own solution, or use Splunk
 - CB Defense has an open API and prebuilt integration with Splunk and SolarWinds
 - CB console has "direct action", such as SSH and modifications, but does not have any device control like disabling USB/CD-ROM. 
   - Device control is this fashion is poised for Q4 release and is on their Roadmap
 - Is *not* sold on a per-month per-seat basis, but rather a per-seat **per-year** basis.

Pricing:

In a hypothetical, say, that we are a reseller with 200 endpoints for two clients. Each of the two clients needs 100 endpoints each. See below for pricing according to this model.
 - MSRP: $46.20 per seat per year
 - Resell: $3200 per year
 - MSSP Partner Resell (with est. 35% discount): $2900 per year

Carbon Black offers a 15 day free trial for their CB Defense.

Carbon Black's CB Defense is often characterized by its administrators as a service that requires high amounts of configuration, or "tuning", but will run fairly hands-free after that initialization. 

Carbon Black's **CB Defense** Next-Gen Anti Virus (NGAV) add-on for Splunk allows administrators to forward events and notifications into Splunk for correlation, aggregation, and analysis.

The CB Defense package is NGAV + EDR which allows signature collection and logging both online and offline. CB Defense uses cloud-based signature-based threat detection using their "Streaming Prevention" against their "Predictive Security Cloud". Data records of offline computers will be synced back to CB Defense and Splunk once the device returns online. The Streaming Defense service works by scoring on-going actions, and terminating the processes once the score reaches "critical". Administrators can isolate endpoints, blacklisting applications, or terminate running processes from the CB Defense control panel or from Splunk. Quarantined or isolated devices can still be SSH'd into for remediation. 

CB Defense would completely replace our traditional BitDefender AV on all endpoints as part of our enhanced cybersecurity package, and the whole system operates from one agent per endpoint thats boasts a less than one percent CPU and disk utilization.

CB Defense requires at least one engineer to be certified in advanced management of the CB Defense product, which is a self-paced 6 hour course, at the end of which follows an untimed, open-book exam. All at no additional cost.

Available on the following platforms:
 - Windows 7/8/10
 - Mac OS X 10.6.8+
 - Windows Server 2008 R2
 - Windows Server 2012, 2012 R2
 - Windows Server 2016
 - Windows Server 2019

Pros:
 - While it does require a higher initial time investment to get it going, it is relatively hands-off after init config
 - Customized policies that go far beyond toggle switches for policies

Cons:

 - Carbon Black's CB Defense had the highest amount of false positive's of any tested EDR product, with NSS Labs evaluating the type I error rate at 0.6%. All other tested products had either a 0% or a 0.1% false positive rate. 
 - A newer acquisition, so relatively untested in production environments when compared to SentinelOne or Crowdstrike or Cisco AMP, etc. Although this service is still one of the most highly rated out there, it replaced CB's native Confer service.
 - No Linux support for Response part of EDR - can only monitor and prevent alone. 
 - Pricing is per-seat per-**YEAR**

___


### Crowdstrike's **Falcon Point**

- [Crowdstrike Falcon Complete Data Sheet](https://www.crowdstrike.com/wp-content/brochures/datasheets/falcon_endpoint_protection_complete.pdf)

Requirements, met, unmet:
 - CS Falcon is entirely cloud-based
 - They do have an MSSP reseller program, which offers some form of discount, but has at least 1000+ endpoints under management and an upfront purchase of 250 licenses
 - Multi-tenancy is there.
 - Can be integrated with Splunk, as Splunk is the backend of CS's EDR instance
 - Has an open API, and we can develop our own solution, or use Splunk
 - CS Falcon has an open API and prebuilt integration with Splunk
 - CS Falcon has "direct action"
 - Is *not* sold on a per-month per-seat basis, but rather a per-seat **per-year** basis.


Crowdstrike offers a 15 day free trial for their NGAV

Crowdstrike's NGAV+EDR, called **Falcon Strike**, is available as tiers:
 - Falcon Pro - $6.99 per month per endpoint
 - Falcon Enterprise - $14.99 per endpoint per month
 - Falcon Premium - $17.99 per endpoint per month 
 - Falcon Complete - Inquire about pricing

Only Enterprise tier and above include the EDR. The Complete tier is purchased as security as a service. 

Crowdstrike has written a series of add-ons to facilitate integration with Splunk. 

Typically, Crowdstrike's Falcon NGAV+EDR is suggested to run *on top* on traditional AV. Crowdstrike is also the best in the game when it comes to preventing malicious PowerShell execution. Installation can be password-protected so that it cannot be uninstalled, even with local administrator privileges. 

CS also has true quarantine, where CB would only delete malware or malicious script. The true quarantine process of CS allows for recovery of the file or even the malware. 

Re-selling/Partnering
 - Crowdstrike has a reseller program that requires OSI to meet the following requirements:
    - MSSSP needs at least 1000 endpoints under management 
    - MSSSP must make a minimum upfront purchase of at least 250 endpoint licenses


Available on the following platforms
 - Windows 7/8/10
 - MacOS
 - Linux
 - Windows Server (unspecified)

Cons:

 - EDR does not have capability to scan a host prior to being installed on said host. 
 - Falcon does not have any "heartbeat" records - "X machine has not checked in in X hours."
 - Crowdstrike does not offer an .msi installer, and instead recommends that an outdated GPO deployment strategy via logon scripts
    - "windowssensor.exe /install /quiet /norestart" supposedly installs the agent, as per their documentation, without issue or interruption
 - Dont provide their full product and services to MSPs, undercutting of own MSP businesses by taking their customers.
 



___


### SentinelOne's **EPP** - (Endpoint Protection Platform)
 - [SentinelOne EPP Datasheet](https://go.sentinelone.com/rs/327-MNM-087/images/SEN0202_DataSheet_EPP_WEB.pdf)

SentinelOne's Endpoint Protection Platform (EPP) is their flagship program, and is highly rated by NSS labs. It does offer integration with Splunk, and EPP can be either cloud-based or on-prem deployment.

SentinelOne, or S1 for short, is actually known for their very robust API for Splunk integration (or any other third party platform).

One exciting feature is the "Attack Storyline", which is a forensic representation of what the attack did chronologically. This will include what processes were called, and what process those processes called, in addition to various metrics like raw data and file statistics. 

SentinelOne has a partnership with SolarWinds and will be able to re-sell SolarWinds and vice-versa. We can pick up SentinelOne for a per-seat per-month basis for all licenses fewer than 3000 in quantity. Anything over 3000 in quantity will go through SentinelOne

Does have a re-seller agreement that we could sign up with. 

Best of all the ransomware warranties

SentinelOne has a partner portal with training videos, and will be deploying a formal training program at the end of this year, being built out right now. Currently, only training videos and documentation. 

Available on the following platforms 
 - Winows 7/8/10
 - MacOS X 10.9+
 - CentOS, RHEL 6.5, 7.0, 7.2
 - Ubuntu 12.04, 14.04, 16.04, 16.10
 - Windows Server 2003
 - Windows Server 2008, 2008 R2
 - Windows Server 2012, 2012 R2
 - Windows Server 2016
 - VMware vSphere, etc.

Joe Zingarelli - head of MSP deployment for SentinelOne - SentinelOne has specific deployment procedures and pricing for MSPs.

Gabe Sechrest -  Inside Sales Rep

Pros: 
 - Can be purchased directly through SolarWinds
 - Is one of the cheaper options 
 
Cons: 
 - 

___

### Palo Alto Networks' **Traps**

 - [Palo Alto Traps Datasheet](https://www.paloaltonetworks.com/resources/datasheets/endpoint-protection)

Palo Alto Traps is Palo Alto's EDR, and it is a cloud-based behavioral-analysis software through endpoint agents that predict and prevent suspecct code execution and malware.

 - Partner program for MSPs is extrememly difficult to get into, since they currently have so many. [Most information can be found here](https://www.paloaltonetworks.com/partners/become-a-partner)
 - Multi-Tenancy is available only with a minimum of 200 endpoints.
 - Cannot block full functionality of USB/CD-ROM ports, but can prevent an executable from running.
 - Licensing is on a per-seat per-year basis.  

A demo will be done by a Jessica Broderick.
Available on the following platforms:
 - Windows
 - MacOS
 - Linux
 - Android
