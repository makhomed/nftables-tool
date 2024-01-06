nftables-tools (version 1.2.0)
==============================

Generate /etc/sysconfig/nftables-allowed-ipv4.conf and /etc/sysconfig/nftables-allowed-ipv6.conf

By default, include to list of allowed IPv4 addresses only Cloudflare IPv4 addresses.

By default, include to list of allowed IPv6 addresses only Cloudflare IPv6 addresses.

But, also it is possible to add extra IPv4 and/or IPv6 subnets in CIDR notation via command line.

Installation
------------

- ``cd /opt ; git clone https://github.com/makhomed/nftables-tool.git``
- ``yum install python3 python3-pip``
- ``python -m pip install --upgrade-strategy eager --upgrade Jinja2 requests invoke``

Upgrade
-------

- ``cd /opt/nftables-tool ; git pull``
- ``python -m pip install --upgrade-strategy eager --upgrade Jinja2 requests invoke``

Usage
-----

.. code-block:: none

    /opt/nftables-tool/nftables-tool

or

.. code-block:: none

    /opt/nftables-tool/nftables-tool 172.21.0.0/16 2001:DB8:1111:2222::/64 2001:DB8:9999:7777::/64

Automation via cron
-------------------

Configure cron job, for example, in file ``/etc/cron.d/nftables-tool``:

.. code-block:: none

    RANDOM_DELAY=360
    0 0 * * * root /opt/nftables-tool/nftables-tool

or

.. code-block:: none

    RANDOM_DELAY=360
    0 0 * * * root /opt/nftables-tool/nftables-tool 172.21.0.0/16 2001:DB8:1111:2222::/64 2001:DB8:9999:7777::/64

