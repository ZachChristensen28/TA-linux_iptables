# Lookup table files

This add-on uses a few CSV lookup files to enrich the data. See below for more information on the lookups used.

Lookup | Lookup definition | Description
------ | ----------------- | -----------
iptables_action.csv | iptables_action_lookup | Used to map events to their appropriate action. This utilizes default Firewalld and UFW log prefixes. Custom log prefixes will need to be setup for this to work see [Using custom log prefixes](../../guides/guide-custom-log-prefix) for more information.
iptables_frametypes.csv | iptables_frametypes_lookup | Maps Frame Type codes to their descriptive value.
iptables_icmp_codes.csv | iptables_icmp_codes_lookup | Maps ICMP codes to their descriptive value.
iptables_transport.csv | iptables_transport_lookup | Used to map the transport field to the CIM-compliant value.

--8<-- "includes/abbreviations.md"