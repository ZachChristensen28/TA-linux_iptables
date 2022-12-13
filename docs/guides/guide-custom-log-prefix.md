# Custom Log Prefix

If you wish to utilize custom log prefixes for use cases, additional setup will be needed for this add-on to properly identify events.

This add-on uses the following to map events to their appropriate CIM-compliant action. The action field is important for the Network Traffic data model. If the log prefix does not match your events, the action will be "unknown."

Log Prefix | Action
---------- | ------
\*allow\* | allowed
\*block\* | blocked
\*drop\* | blocked
\*accept\* | allowed
\*reject\* | blocked
\*permit\* | allowed
\*deny\* | blocked
\*denied\* | blocked

_<small>the wildcard character (*) is used to find any match with the contained value in the `log_prefix` field.</small>_

## Use your own log prefix

It is recommended to use the log prefixes in the above table somewhere in your custom log prefix so no extra work is needed.

???+ example
    "**allow**\_ssh\_connections" or "telnet\_**drop**"

### Add new log prefix definition

If the above table defaults do not work for your use case, another lookup can be created with the correct values to fit your situation.

???+ question "Why use a new lookup file?"
    If the existing lookup file is used, it will be overwritten during future updates. To preserve changes, a new lookup file must be created.

It may be easiest to to utilize the linux command line to copy the lookup file, `iptables_action.csv` located in the `lookups` directory within this add-on.

???+ example

    ```shell
    cp lookups/iptables_actions.csv lookups/iptables_custom_actions.csv
    ```

From there you can update the file to fit your use case.

???+ example "Updating lookup example"

    ```shell
    log_prefix,action
    *mycustom_allow*,allowed
    *custom_reject*,blocked
    *custom_drop*,blocked
    ```

It is recommended to have the action field mapped to the [Network Traffic](https://docs.splunk.com/Documentation/CIM/4.20.0/User/NetworkTraffic) datamodel action field (allowed, blocked, teardown). Wrapping the `log_prefix` field in wildcards (*) gives the flexibility of not having to specify exact values.

#### Update transforms.conf

After the custom lookup file has been updated, the transforms.conf file will need to be updated to the correct filename.

Within the add-on, create a new file in `local/transforms.conf` (you may have to create the local directory). Next add the following to the file:

```ini title="local/transforms.conf"
[iptables_action_lookup]
# If you followed the above example you would
# set this to "iptables_custom_actions.csv" (without quotations).
filename = <your_new_file.csv>
```

Once the change has been made it may take a few minutes for the changes to take effect. If you don't want to wait you can append `| extract reload=true` to your Splunk search to force a reload of the configurations. You should now see the correct actions being populated and no longer will show "unknown."

--8<-- "includes/abbreviations.md"
