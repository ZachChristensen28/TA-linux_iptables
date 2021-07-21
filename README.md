# TA-linux_iptables - Add-on for Linux Iptables

![GitHub](https://img.shields.io/github/license/zachchristensen28/TA-linux_iptables)
[![Documentation Status](https://readthedocs.org/projects/splunk-iptables-ta-documentation/badge/?version=latest)](https://splunk-iptables-ta-documentation.readthedocs.io/en/latest/?badge=latest)

Info | Description
------|----------
Version | 1.3.6 - See on [Splunkbase](https://splunkbase.splunk.com/app/4490/)
Vendor Product | RHEL/CentOS - Firewalld, Ubuntu - UFW, built-in IPtables
Add-on has a web UI | No. This add-on does not contain any views.

The TA-linux_iptables Add-on allows Splunk data administrators to map the linux firewall events to the [CIM](https://docs.splunk.com/Splexicon:CommonInformationModel) enabling the data to be used with other Splunk Apps, such as Enterprise Security.

## Release Notes

```
Version: 1.3.6

Notice:
   This updated simplifies the number of sourcetypes down to a single sourcetype (linux:iptables). Any existing reports/alerts/views that are utilizing the old sourcetypes ("linux:iptables:ufw" or "linux:iptables:firewalld") will be impacted. Verify before updating to this version. 

- added support for firewalld rich rules - #2
- updated to only use the single sourcetype, 'linux:iptables'
- updated action lookup to use wildcards
```

## Documentation

Full documentation can be found at https://splunk-iptables-ta-documentation.rtfd.io.


## Issues or Feature Requests

Please open an issue or submit feature requests at [github.com](https://github.com/ZachChristensen28/TA-iptables)

