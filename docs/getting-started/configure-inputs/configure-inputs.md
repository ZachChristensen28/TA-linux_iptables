# Configure Splunk Input

**Objective**: Set the sourcetype to `linux:iptables` in the inputs.conf file on the forwarder.

## Create a new index

!!! info "Optional Step"
    If you do not wish to create a new index, skip to [Splunk Universal Forwarder Configuration](#splunk-universal-forwarder-configuration).

Splunk stores data in indexes. This add-on may be configured to send to a custom event index instead of the default index, main. For more information and steps to create a new index, see [Splunk Docs: Create events indexes](https://docs.splunk.com/Documentation/Splunk/latest/Indexer/Setupmultipleindexes#Create_events_indexes_2).

### Purpose for Creating a new index

The out of the box Splunk configuration stores all data in the default index, main. It is encouraged to create a new index to ensure optimal performance, for setting retention policies, and for providing stricter access controls. For more information about how Splunk indexes work with add-ons, see [Splunk Docs: Add-ons and indexes](https://docs.splunk.com/Documentation/AddOns/released/Overview/Add-onsandindexes).

## Splunk Universal Forwarder Configuration

Download the latest [Splunk Universal Forwarder (UF)](https://www.splunk.com/en_us/download/universal-forwarder.html) appropriate for your server.

!!! note
    Unless utilizing a syslog server, this UF should be installed on the same server that you wish to collect linux firewall events from.

Install the UF according to [Splunk Docs: Install the Universal Forwarder](https://docs.splunk.com/Documentation/Forwarder/latest/Forwarder/Installtheuniversalforwardersoftware).

Once installed the configurations can be made. The following is a sample inputs.conf that can be pushed using a deployment server or configured on the UF itself.

```cfg title="inputs.conf"
[monitor:///var/log/iptables.log]
disabled = 0
sourcetype = linux:iptables
# optionally specify an index, if configured.
index = osnixfw
```

The above assumes the iptable logs have been split into a separate file (see [Prepare Logs for Splunk](../../prepare-logs-for-splunk/#syslog-setup)). If the iptable logs are mixed with other linux logs, then use the following sample configuration as a guide.

### Mixed Logs

``` cfg title="inputs.conf - for mixed logs"
[monitor:///var/log/syslog]
disabled = 0
sourcetype = syslog
# optionally specify an index, if configured.
index = osnix
```

Then create a local directory within this app and add a props.conf to transform the sourcetype to the correct sourcetype.

``` cfg title="local/props.conf - needed for mixed logs"
[syslog]
TRANSFORMS-iptables_sourcetyper = iptables_sourcetyper
```

This will enable a prebuilt transforms to automatically sourcetype these logs.

Push the configuration to the forwarder, if using a deployment server, or restart the UF if configuring on the UF itself.

## Verify

Verify the setup has completed successfully by navigating to Splunk web and running a search similar to the following:

```text
index=<chosen index> sourcetype=linux:iptables
```

If you see data then you are all set! If you are not seeing your data, see [Troubleshooting Monitoring Inputs](../troubleshooting/troubleshoot-inputs.md).

--8<-- "includes/abbreviations.md"
