# TA-linux_iptables - Add-on for Linux Iptables

![GitHub](https://img.shields.io/github/license/zachchristensen28/TA-linux_iptables)

Info | Description
------|----------
Version | 1.3.6 - See on [Splunkbase](https://splunkbase.splunk.com/app/4490/)
Vendor Product | RHEL/CentOS - Firewalld, Ubuntu - UFW, built-in IPtables
Add-on has a web UI | No. This add-on does not contain any views.

The TA-linux_iptables Add-on allows Splunk data administrators to map the linux firewall events to the [CIM](https://docs.splunk.com/Splexicon:CommonInformationModel) enabling the data to be used with other Splunk Apps, such as Enterprise Security.

## Release Notes

```
Version: 1.3.6

- added support for firewalld rich rules - #2
- updated to only use single sourcetype 'linux:iptables'
- updated action lookup to use wildcards 
```

### Where to Install

Splunk platform Instance type | Supported | Required | Actions required/ Comments
----------------------------- | --------- | -------- | --------------------------
Search Heads | Yes | Yes | Install this add-on to all search heads
Indexers | Yes | Conditional | Not required if heavy forwarders are used to collect data. Required if using Universal or Light Forwarders.
Heavy Forwarders | Yes | Conditional | Required, if HFs are used to collect this data source.

\* For more information, see Splunk's [documentation](https://docs.splunk.com/Documentation/AddOns/released/Overview/Installingadd-ons) on installing Add-ons.

## Input Setup

### Uncomplicated Firewall (UFW)

UFW handles logging of firewall rules. There would be no need to complete the following sections. Simply set the sourcetype to `linux:iptables` and the add-on will take care of the rest.

### Input Requirements (non-UFW)

Set the sourcetype to "linux:iptables" in the inputs.conf file on the forwarder (see [recommendations below](#recommendations-for-iptables-logging)).

i.e.

```
# Sample inputs.conf

[monitor:///var/log/iptables.log]
disabled = 0
sourcetype = linux:iptables
```

### Built-in Iptable Requirements

If the iptables "log prefix" flag is utilized, further setup may be needed to have the log_prefix field extracted correctly. This will be built into the add-on in future releases. For now, the transforms.conf file will need to be modified to extract this field correctly.

The add-on currently supports the following syntax for the log_prefix field.

```
... ** My log prefix ** ...
```

Where "My log prefix" will be the field extracted. In the likely event that this does not match the current configurations, modify `../local/transforms.conf` with the correct regex needed.

i.e.

```
# ../local/transforms.conf

[iptables_log_prefix]
REGEX = CUSTOM REGEX HERE
FORMAT = log_prefix::$1
```

## Recommendations for iptables logging

Depending on how logging is setup on the linux instance, iptable logs could be writing to the kern.log or syslog. If needed, syslog could be sent directly to splunk and this add-on will transform the sourcetype to linux:iptables (see [Syslog support](#syslog-support) below).

It is recommended to have iptable logs write to it's own file in /var/log. This can be achieved by modifying the configuration files for the type of syslog being used. See the docs for the respective syslog being used.

#### Example for setting up rsyslog to write to it's own file on Ubuntu
Create a new configuration in /etc/rsyslog.d/
You can copy an existing configuration already in that directory to simplify the process.

i.e.

```
# Example configuration file
# /etc/rsyslog.d/10-iptables.conf

# Log iptables log messages to file
:msg,regex,"IN=[^\=]*OUT=" /var/log/iptables.log

# The following stops logging anything that matches the last rule to the original file being logged to.
& stop
```

The above example is matching a unique string for linux iptables and will place each match into "/var/log/iptables.log"


### Syslog support

 For this to work, copy the `syslog` stanza from `../default/props.conf` of this app and add it to the `../local/props.conf` file. 

i.e.

```
# ../local/props.conf

[syslog]
TRANSFORMS-iptables_sourcetyper = iptables_sourcetyper, iptables_ufw_sourcetyper, iptables_firewalld_sourcetyper
```

## Additional Required Setup

For the "action" field to work properly, the lookup (iptables_action.csv) will need to be modified to the correct log-prefix that are currently setup in the iptables environment. This informs splunk of the action the iptables took. Failing to do so will result in the action field being "unknown". The appropriate fields to map to would be allowed|blocked|teardown.

## Sourcetype

The following are sourcetypes this add-on automatically identifies. These sourcetypes do not need to be set manually.

Source Type | Description | CIM Data Models
----------- | ----------- | ---------------
`linux:iptables` | Used for built-in iptables | [Network Traffic](https://docs.splunk.com/Documentation/CIM/latest/User/NetworkTraffic)
`linux:iptables:ufw` | Default on Ubuntu distros | [Network Traffic](https://docs.splunk.com/Documentation/CIM/latest/User/NetworkTraffic)
`linux:iptables:firewalld` | Default on RHEL/CentOS | [Network Traffic](https://docs.splunk.com/Documentation/CIM/latest/User/NetworkTraffic)


## Bugs
Please open an issue at [github.com](https://github.com/ZachChristensen28/TA-iptables)

