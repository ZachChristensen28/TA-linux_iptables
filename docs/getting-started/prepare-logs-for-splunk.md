# Prepare Logs for Splunk

!!! info "Optional"

## Syslog Setup

To simplify logging of linux firewall events it is recommended to utilize rsyslog, syslog-ng, or a similar tool to separate firewall events into a new file for Splunk to monitor.

Refer to the vender specific documentation on the best-practices to accomplish this. A simple example using rsyslog is demonstrated below.

???+ example "Rsyslog Example"

    ```shell
    # Example configuration file
    # /etc/rsyslog.d/10-iptables.conf

    # Log iptables log messages to file
    :msg,regex,"IN=[^\=]*OUT=" /var/log/iptables.log

    # The following stops logging anything that matches the last rule to the original file being logged to.
    & stop
    ```

!!! note
    Verify the created file will have sufficient privileges for Splunk to monitor the file.

## Log Prefix

By default UFW and Firewalld use their own log prefixes:

 Firewall | Prefix | Example
 -------- | ------ | -------
 UFW | `[UFW *]` | `[UFW ALLOW] IN= OUT=eth0 SRC=192.168.0.15 DST=192.168.0.16 LEN=76 TOS=0x10 PREC=0x00 TTL=64 ID=32137 DF PROTO=UDP SPT=36231 DPT=123 LEN=56`
 Firewalld | `*_DROP` or `*_REJECT` | `FINAL_REJECT: IN=ens192 OUT= MAC= SRC=10.0.10.10 DST=10.0.10.21 LEN=328 TOS=0x00 PREC=0x00 TTL=57 ID=4162 PROTO=UDP SPT=53483 DPT=38811 LEN=308`

 If custom log prefixes are being used, additional setup may be required for this add-on to work appropriately. See [Using Custom Log Prefixes](../../guides/guide-custom-log-prefix) in this documentation for more information.

--8<-- "includes/abbreviations.md"
