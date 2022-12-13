# TA-linux_iptables - Add-on for Linux Iptables

[![TA-linux_iptables](./docs/assets/images/linux-iptables-large.png)](https://splunk-iptables.ztsplunker.com)

![GitHub](https://img.shields.io/github/license/zachchristensen28/TA-linux_iptables)
[![Documentation Status](https://github.com/ZachChristensen28/TA-linux_iptables/actions/workflows/docs-caller.yml/badge.svg)](https://splunk-iptables.ztsplunker.com)
![Appinspect](https://github.com/ZachChristensen28/TA-linux_iptables/actions/workflows/appinspect.yml/badge.svg)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/ZachChristensen28/TA-linux_iptables)
[![Splunkbase App](https://img.shields.io/badge/Splunkbase-TA--linux__iptables-blue)](https://splunkbase.splunk.com/app/4490/)
[![Splunk CIM Version](https://img.shields.io/badge/Splunk%20CIM%20Version-5.x%20|%204.x-success)](https://docs.splunk.com/Documentation/CIM/latest/User/Overview)

## Documentation

Full documentation can be found at [https://splunk-iptables.ztsplunker.com](https://splunk-iptables.ztsplunker.com).

## About

Info | Description
------|----------
Version | 1.3.8 - See on [Splunkbase](https://splunkbase.splunk.com/app/4490/)
Vendor Product | RHEL/CentOS - Firewalld, Ubuntu - UFW, built-in IPtables
Add-on has a web UI | No. This add-on does not contain any views.

The TA-linux_iptables Add-on allows Splunk data administrators to map the linux firewall events to the [CIM](https://docs.splunk.com/Splexicon:CommonInformationModel) enabling the data to be used with other Splunk Apps, such as Enterprise Security.

## Release Notes

```text
Version: 1.3.8

- Added sample configuration for the syslog sourcetype if IPtable data is mixed with syslog data.
- Updated log_prefix field extraction to consider log prefixes surrounded with quotes.
```

## Issues or Feature Requests

Please open an issue or submit feature requests at [GitHub](https://github.com/ZachChristensen28/TA-iptables/issues)
