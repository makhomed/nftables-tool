nftables-tool (version 1.2.0)
=============================

Generate /etc/sysconfig/nftables-allowed-ipv4.conf and /etc/sysconfig/nftables-allowed-ipv6.conf

By default, include to list of allowed IPv4 addresses only Cloudflare IPv4 addresses.

By default, include to list of allowed IPv6 addresses only Cloudflare IPv6 addresses.

But, also it is possible to add extra IPv4 and/or IPv6 subnets in CIDR notation via command line.

See `contrib/nftables.conf <https://github.com/makhomed/nftables-tool/blob/master/contrib/nftables.conf>`_ for example of usage of these generated ipv4_addr / ipv6_addr sets.

See also the `nginx-cloudflare tool<https://github.com/makhomed/nginx-cloudflare>`_, which can be used instead of nftables-tool, if the Linux server must simultaneously allow two types of connections - both direct connections from clients and connections only from Cloudflare networks - in this case, filtering is applied at the nginx level through the geo module.

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

    /opt/nftables-tool/nftables-tool 172.21.0.0/16 2001:DB8:11:22::/64 2001:DB8:99:77::/64

Automation via cron
-------------------

Configure cron job, for example, in file ``/etc/cron.d/nftables-tool``:

.. code-block:: none

    RANDOM_DELAY=360
    0 0 * * * root /opt/nftables-tool/nftables-tool

or

.. code-block:: none

    RANDOM_DELAY=360
    0 0 * * * root /opt/nftables-tool/nftables-tool 172.21.0.0/16 2001:DB8:11:22::/64 2001:DB8:99:77::/64

