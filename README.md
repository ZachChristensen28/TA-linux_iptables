# TA-iptables
Splunk Add-on for Linux Iptables

## Sourcetype

```
linux:iptables
```

### Where to Install
Splunk platform Instance type | Supported | Required | Actions required/ Comments
----------------------------- | --------- | -------- | --------------------------
Search Heads | Yes | Yes | Install this add-on to all search heads
Indexers | Yes | Conditional | Not required if heavy forwarders are used to collect data.
Heavy Forwarders | Yes | Conditional | Not required.

\* **This add-on must be installed on either the HF or Indexers.**

## Input Requirements
Set the sourcetype to "linux:iptables" in the inputs.conf file on the forwarder (see [recommendations below](#recommendations-for-iptables-logging)).

i.e.

```
# Sample inputs.conf

[monitor:///var/log/iptables.log]
disabled = 0
sourcetype = linux:iptables
```

### Iptable Requirements
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

### Recommendations for iptables logging
Depending on how logging is setup on the linux instance, iptable logs could be writting to the kern.log or syslog. If needed, syslog could be sent directly to splunk and this add-on will transform the sourcetype to linux:iptables (see [Syslog support](#syslog-support) below).

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
 For this to work, the props.conf file will need to be modified to accept the syslog sourcetype. Simply enable the syslog source type in ../local/props.conf then restart splunk

i.e.

```
# ../local/props.conf

[syslog]
disabled = false
```

## Bugs
Please open an issue at [github.com](https://github.com/ZachChristensen28/TA-iptables)
