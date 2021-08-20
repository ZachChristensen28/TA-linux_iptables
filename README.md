# TA-linux_iptables - Add-on for Linux Iptables

![GitHub](https://img.shields.io/github/license/zachchristensen28/TA-linux_iptables)
[![Documentation Status](https://readthedocs.org/projects/splunk-iptables-ta-documentation/badge/?version=latest)](https://splunk-iptables-ta-documentation.readthedocs.io/en/latest/?badge=latest)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/ZachChristensen28/TA-linux_iptables)
[![Splunkbase App](https://splunkbase.splunk.com/app/4490/)](https://img.shields.io/badge/Splunkbase-TA--linux__iptables-blue)

Info | Description
------|----------
Version | 1.3.7 - See on [Splunkbase](https://splunkbase.splunk.com/app/4490/)
Vendor Product | RHEL/CentOS - Firewalld, Ubuntu - UFW, built-in IPtables
Add-on has a web UI | No. This add-on does not contain any views.

The TA-linux_iptables Add-on allows Splunk data administrators to map the linux firewall events to the [CIM](https://docs.splunk.com/Splexicon:CommonInformationModel) enabling the data to be used with other Splunk Apps, such as Enterprise Security.

## Release Notes

```text
Version: 1.3.7

- fixed incorrect app value for UFW events - #5
- updated regex for different UFW log formats - #8
```

## Documentation

Full documentation can be found at https://splunk-iptables-ta-documentation.rtfd.io.

## Issues or Feature Requests

Please open an issue or submit feature requests at [github.com](https://github.com/ZachChristensen28/TA-iptables)
