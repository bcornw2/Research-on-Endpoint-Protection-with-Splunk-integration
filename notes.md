## Notes on EDR Endpoint Protection

**Conditions**

 - 100% cloud based, no on-prem server hardware or software
 - Moves beyond simple AV to endpoint detection and response (EDR) type capabilities
 - On the business side, they have some kind of reseller program we can sign up with
 - Multi-tenancy allowing us to view all clients on one dashboard through a “single pane of glass”
 - Integration with splunk that is capable enough for us not to have to do any monitoring of the endpoint console itself
 - Ideally, some kind of webhook/api capability so Splunk can be used to trigger actions on workstations
 - The ability to do some device management, perhaps restrict external storage/usb devices
 - That’s a good start. They should all be sold on a per seat per month pricing structure, once you have a few contenders you’d need to reach out to them to see what that looks like.
 
Perhaps do a first pass to see if you can find any other contenders and let me know what the final list of potential options looks like, you can then start researching/testing them in more detail.
 - [NSS Labs Advanced Endpoint Protection Deep-Dive](https://www.nsslabs.com/security-value-maps/advanced-endpoint-protection-aep/)
 - Takeaways:
   - Carbon Black's CB Defense -  the highest cost of the proposed options with a Total Cost of Ownership (TCO) of $245, and had an above average security effectiveness of 93.6%
   - SentinelOne had a below average TCO of $148, with an above average security effectiveness of 97.7%
   - Crowdstrike was not tested
   - Other noteworthy options are Trend Micro, EnSilo, and Palo Alto Networks
___

#### Use Cases

This service should integrate with Splunk SIEM and provide Anti-virus and EDR to our clients. 

There will be only one or two people managing the SIEM server and the security monitoring for the clients who choose to upgrade to the enhanced security package. For the majority of our clients, PHI or PCI data will not be a factor. While we do execute routine vulnerability management scans, we have not been audited by any network security service and OSIbeyond has not been pentested.
___

### Carbon Black's **CB Defense**

 - [Carbon Black CB Defense Datasheet](https://www.carbonblack.com/wp-content/uploads/2018/12/CB_Defense_DataSheet_122018_RGB.pdf)

Carbon Black offers a 15 day free trial for their CB Defense

Carbon Black's CB Defense is often characterized by its administrators as a service that requires high amounts of configuration, or "tuning", but will run fairly hands-free after that initialization. 

Carbon Black's **CB Defense** Next-Gen Anti Virus (NGAV) add-on for Splunk allows administrators to forward events and notifications into Splunk for correlation, aggregation, and analysis.

The CB Defense package is NGAV + EDR which allows signature collection and logging both online and offline. CB Defense uses cloud-based signature-based threat detection using their "Streaming Prevention" against their "Predictive Security Cloud". Data records of offline computers will be synced back to CB Defense and Splunk once the device returns online. The Streaming Defense service works by scoring on-going actions, and terminating the processes once the score reaches "critical". Administrators can isolate endpoints, blacklisting applications, or terminate running processes from the CB Defense control panel or from Splunk. Quarantined or isolated devices can still be SSH'd into for remediation. 

[Carbon Black CB Defense NGAV+EDR](https://www.carbonblack.com/wp-content/uploads/2018/12/CB_Defense_DataSheet_122018_RGB.pdf)

CB Defense would completely replace our traditional BitDefender AV on all endpoints as part of our enhanced cybersecurity package, and the whole system operates from one agent per endpoint thats boasts a less than one percent CPU and disk utilization.

Available on the following platforms:
 - Windows 7/8/10
 - Mac OS X 10.6.8+
 - Windows Server 2008 R2
 - Windows Server 2012, 2012 R2
 - Windows Server 2016
 - Windows Server 2019

Cons:

 - Carbon Black's CB Defense did have the highest amount of false positive's of any tested EDR product, with NSS Labs evaluating the type I error rate at 0.6%. All other tested products had either a 0% or a 0.1% false positive rate. 
 - A newer acquisition, so relatively untested in production environments when compared to SentinelOne or Crowdstrike or Cisco AMP, etc. Although this service is still one of the most highly rated out there, it replaced CB's native Confer service.
 - Known to have problems with Mac as the agents for Mac are on a different release schedule than the Windows agents. 


___


### Crowdstrike's **Falcon Point**

- [Crowdstrike Falcon Complete Data Sheet](https://www.crowdstrike.com/wp-content/brochures/datasheets/falcon_endpoint_protection_complete.pdf)

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
 - CS is noted to have a lack of client-side tools - it does a bad job of managing the entire environment. For example, there is no way to see how many systems currently do not have it installed. Or how many have it installed with no process running. No such "heartbeat" records - "X machine has not checked in in X hours."
 - Crowdstrike does not offer an .msi installer, and instead recommends that an outdated GPO deployment strategy via logon scripts
    - "windowssensor.exe /install /quiet /norestart" supposedly installs the agent, as per their documentation, without issue or interruption
 



___


### SentinelOne's **EPP** - (Endpoint Protection Platform)
 - [SentinelOne EPP Datasheet](https://go.sentinelone.com/rs/327-MNM-087/images/SEN0202_DataSheet_EPP_WEB.pdf)

SentinelOne's Endpoint Protection Platform (EPP) is their flagship program, and is highly rated by NSS labs. It does offer integration with Splunk, and EPP can be either cloud-based or on-prem deployment.

Available on the following Platforms 
 - Winows 7/8/10
 - MacOS X 10.9+
 - CentOS, RHEL 6.5, 7.0, 7.2
 - Ubuntu 12.04, 14.04, 16.04, 16.10
 - Windows Server 2003
 - Windows Server 2008, 2008 R2
 - Windows Server 2012, 2012 R2
 - Windows Server 2016
 - VMware vSphere, etc.
