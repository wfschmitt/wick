Hostname
========

Sets the hostname and domain.  Supports templates.  Can automatically update the hostname when network connections are made.

* $1            - Hostname to set or template for dynamic hostnames.
* --dynamic     - Option that enables a dynamic hostname.
* --iface=IFACE - Use a specified adapter for retrieving the IP address.

When `--dynamic` is used, the hostname will get updated whenever new DHCP leases are established.

The hostname can be just the "local part" (eg. "machine1") or a fully qualified name (eg. "machine1.example.com").  When fully qualified, this also sets the domain name.  Can be templated.

Templated hostnames can change "app1-{{IP}}.example.com" into "app1-192_168_0_1.example.com".  This is not the same template system that formulas use; it is a simple string replacement.  Templated variables that are supported:

* `{{IP}}`:  Results in a string of the current IP address of the machine, with dots replaced by underscores.

When using templated hostnames, you will likely want to also use `--dynamic` so the name is changed after reboots.

Examples

    # Set the hostname to "machine1"
    wickFormula hostname machine1

    # Set the hostname to something like "app1-192-168-0-1.example.com"
    wickFormula hostname --dynamic app1-{{IP}}.example.com

    # Set the hostname as above but specify a network adapter instead
    # of picking one arbitrarily.
    wickFormula hostname --dynamic app1-{{IP}} --iface=eth0

Returns nothing.


