Neutron diagnostics
===================

## gather-network-info

**NB: This script must be run as `root`**

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

You might run it like this:

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

    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/net-3ff9b903-e921-4752-a26f-cba8f1433992.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/net-9624fa1b-aae7-4670-932a-733653fec250.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/net-a2be4bdd-a44a-4e64-ab16-a3297e479a31.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/net-ad1a977e-8a5f-4a22-b445-742094cde1f2.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/net-list.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/router-0511d9f6-9920-4203-bb58-11d505fd4399-ports.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/router-0511d9f6-9920-4203-bb58-11d505fd4399.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/router-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3-ports.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/router-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/router-list.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/subnet-936fd308-f491-400e-8c89-206d39e00a9f.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/subnet-a8553c6d-ebea-4511-b422-50be036bbd3f.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/subnet-c6c15f96-b09c-44d7-beba-e09895e4ae82.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/subnet-cae5afad-217c-4e8b-8413-cdbce5214a5d.txt
    neutron-lkellogg-pk115wp-2013-12-20T14-26-02/subnet-list.txt

## Reporting bugs

If you encounter problems with either of these scripts or if you have
suggestions for ways they could be improved, please feel free to open
an issue in the [issue tracker](https://github.com/larsks/neutron-diag/issues).

## License

neutron-diag -- scripts for gathering information about your Neutron
configuration.  
Copyright (C) 2013 Lars Kellogg-Stedman `<lars@oddbit.com>`

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

