Neutron diagnostics
===================

## gather-network-info

**NB: This script must be run as `root`**

This script gathers network information for all of the active network
namespaces on your system, where "active" in this context means "has
interfaces other than `lo`".  It outputs a tarball in your current
directory named `network-HOST-DATE.tar.gz`.

For each namespace, the script collects information about:

- interfaces and addresses
- routes
- open/listening connections
- processes
- iptables rules

Additionally, the script collects some information from OVS.

You might run it like this:

    sudo ./gather-network-info

The contents of the tarball will look something like this:

    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/routes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/tun0.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/qvo26b806a7-02.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/em1.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/br-int.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/ovs-system.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/qvb26b806a7-02.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/qvb7a02b625-32.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/br-ex.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/tap7a02b625-32.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/tap26b806a7-02.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/qvo7a02b625-32.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/qbr7a02b625-32.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/virbr1.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/wlp3s0.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/virbr2.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/interfaces/qbr26b806a7-02.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/connections/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/connections/tcp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/connections/udp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/iptables/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/iptables/filter.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/global/iptables/nat.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/hostname.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/namespace-active.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/namespace-inactive.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/ovs-bridges.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/ovs-dpctl-show.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/ovs-ofctl-dump-flows-br-ex.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/ovs-ofctl-dump-flows-br-int.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/ovs-vsctl-show.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/routes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/interfaces/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/interfaces/tap786bdb61-98.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/connections/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/connections/tcp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/connections/udp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/processes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/iptables/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/iptables/filter.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-3ff9b903-e921-4752-a26f-cba8f1433992/iptables/nat.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/routes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/interfaces/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/interfaces/tap65db9373-99.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/connections/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/connections/tcp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/connections/udp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/processes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/iptables/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/iptables/filter.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-a2be4bdd-a44a-4e64-ab16-a3297e479a31/iptables/nat.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/routes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/interfaces/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/interfaces/tap7e50b0bb-c5.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/connections/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/connections/tcp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/connections/udp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/processes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/iptables/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/iptables/filter.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qdhcp-ad1a977e-8a5f-4a22-b445-742094cde1f2/iptables/nat.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/routes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/interfaces/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/interfaces/qr-66c6b76e-b7.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/interfaces/qg-3169ffbe-57.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/connections/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/connections/tcp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/connections/udp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/processes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/iptables/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/iptables/filter.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-0511d9f6-9920-4203-bb58-11d505fd4399/iptables/nat.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/routes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/interfaces/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/interfaces/qr-5b52ec34-86.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/interfaces/qg-f69c19b8-5a.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/connections/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/connections/tcp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/connections/udp.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/processes.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/iptables/
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/iptables/filter.txt
    network-lkellogg-pk115wp-2013-12-20T15-55-04/qrouter-2a2b2640-6f9a-42f8-b269-ab8bb5cd9fa3/iptables/nat.txt

## render-network-info

This takes as an argument the tarball produced by
`gather-network-info` and generates Markdown formatted output on
`stdout`.  You can convert this to HTML using any of a variety of
Markdown processes, e.g.:

    ./render-network-info network-lkellogg-pk115wp-2013-12-20T15-55-04.tar.gz |
      marked > network-info.html

## gather-neutron-info

** NB: This script must be run with valid OpenStack credentials `OS_AUTH_URL`, `OS_USERNAME`,
`OS_TENANT_NAME`, etc) in your environment. **

This script gather Neutron configuration information from the
perspective of your current OpenStack credentials.  It outputs a
tarball in your current directory named `neutron-HOST-DATE.tar.gz`.

This scripts collects the output of:

- `neutron net-list`
- `neutron subnet-list`
- `neutron router-list`

...and the corresponding `show` command for each of the networks,
subnets, and routers discovered.  It also collects the output of
`router-port-list` for each router.

Optionally adding `-l` on the command line will cause the script to
package up `/var/log/neutron/*.log` into the tarball as well.  Using
`-l` probably requires that you run this script as `root`.

You might run it like this:

    ./gather-neutron-info

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

## render-neutron-info

This takes as an argument the tarball produced by
`gather-neutron-info` and generates Markdown formatted output on
`stdout`.  You can convert this to HTML using any of a variety of
Markdown processes, e.g.:

    ./render-neutron-info neutron-lkellogg-pk115wp-2013-12-20T15-55-04.tar.gz |
      marked > neutron-info.html

## mk-network-dot

This script generates [dot][] format output representing the
connectivity of network devices and network namespaces on your system.
You can render this output using the `dot` program, part of the
[GraphViz][] package.  For example, to generate SVG output:

    sudo sh mk-network-dot | dot -Tsvg -o network.svg

[dot]: http://en.wikipedia.org/wiki/DOT_%28graph_description_language%29
[graphviz]: http://www.graphviz.org/

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

