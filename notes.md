##Notes on EDR Endpoint Protection

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

___

**Carbon Black**
  Carbon Black's **CB Defense** Next-Gen Anti Virus (NGAV) add-on for Splunk allows administrators to forward events and notifications into Splunk for correlation, aggregation, and analysis.
The CB Defense package is NGAV + EDR which allows signature collection and logging both online and offline. CB Defense uses cloud-based signature-based threat detection using their "Streaming Prevention" against their "Predictive Security Cloud". Data records of offline computers will be synced back to CB Defense and Splunk once the device returns online. The Streaming Defense service works by scoring on-going actions, and terminating the processes once the score reaches "critical". Administrators can isolate endpoints, blacklisting applications, or terminate running processes from the CB Defense control panel or from Splunk. Quarantined or isolated devices can still be SSH'd into for remediation. 

[Carbon Black CB Defense NGAV+EDR](https://www.carbonblack.com/wp-content/uploads/2018/12/CB_Defense_DataSheet_122018_RGB.pdf)

CB Defense would completely replace our traditional BitDefender AV on all endpoints as part of our enhanced cybersecurity package, and the whole system operates from one agent per endpoint thats boasts a less than one percent CPU and disk utilization.

Available on the following platforms:
 - Windows 7/8/10
 - Mac OS X 10.6.8+
 - Windows Server 2008 R2
 - Windwos Server 2012, 2012 R2
 - Windows Server 2016
 - Windows Server 2019

___


