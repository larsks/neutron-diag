Neutron diagnostics
===================

## gather-network-info

This script gathers network information for all of the active network
namespaces on your system, where "active" in this context means "has
interfaces other than `lo`".

For each namespace, the script collects information about:

- interfaces and addresses
- routes
- open/listening connections
- processes
- iptables rules

Additionally, the script collects some information from OVS.

You would run it like this:

    sudo ./gather-network-info > network.md

The output is Markdown formatted, which means you can convert it into
HTML using any of a variety of Markdown processors (e.g.,
`python-markdown`, `marked`, `python-markdown2`, `pandoc`, etc).  For
example, using `marked`:

    marked network.md > network.html

## gather-neutron-info

This script generates a tarball in your current directory called
`neutron-HOST-DATE.tar.gz` (where *HOST* and *DATE* are replaced by
your current hostname and the current date/time) containing the output
of:

- `neutron net-list`
- `neutron subnet-list`
- `neutron router-list`

...and the corresponding `show` command for each of the networks,
subnets, and routers discovered.  It also collects the output of
`router-port-list` for each router.

The contents of the tarball will look something like this:

    net-3ff9b903-e921-4752-a26f-cba8f1433992.txt
    net-9624fa1b-aae7-4670-932a-733653fec250.txt
    net-a2be4bdd-a44a-4e64-ab16-a3297e479a31.txt
    net-ad1a977e-8a5f-4a22-b445-742094cde1f2.txt
    net-list.txt
    router-0511d9f6-9920-4203-bb58-11d505fd4399-ports.txt
    router-0511d9f6-9920-4203-bb58-11d505fd4399.txt
    router-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3-ports.txt
    router-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3.txt
    router-list.txt
    subnet-936fd308-f491-400e-8c89-206d39e00a9f.txt
    subnet-a8553c6d-ebea-4511-b422-50be036bbd3f.txt
    subnet-c6c15f96-b09c-44d7-beba-e09895e4ae82.txt
    subnet-cae5afad-217c-4e8b-8413-cdbce5214a5d.txt
    subnet-list.txt

