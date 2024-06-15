# nftables-tool (version 1.2.3)

Generate `/etc/sysconfig/nftables-allowed-ipv4.conf` and `/etc/sysconfig/nftables-allowed-ipv6.conf`

By default, include to list of allowed IPv4 addresses only Cloudflare IPv4 addresses.

By default, include to list of allowed IPv6 addresses only Cloudflare IPv6 addresses.

But, also it is possible to add extra IPv4 and/or IPv6 subnets in CIDR notation via command line.

See [`contrib/nftables.conf`](https://github.com/makhomed/nftables-tool/blob/master/contrib/nftables.conf)
for example of usage of these generated ipv4_addr / ipv6_addr sets.

See also the [`nginx-cloudflare`](https://github.com/makhomed/nginx-cloudflare), which can be used instead of nftables-tool,
if the Linux server must simultaneously allow two types of connections - both direct connections from clients
and connections only from Cloudflare networks - in this case, filtering can be applied only at the nginx level,
through the geo module.

## Installation
> [!IMPORTANT]
> Python 3.8+ and [Jinja2](https://jinja.palletsprojects.com/), [requests](https://requests.readthedocs.io/), [invoke](https://www.pyinvoke.org/) modules required
```
dnf -y install python3 python3-pip python-unversioned-command ; \
python -m pip install --no-input --upgrade-strategy eager --upgrade Jinja2 requests invoke ; \
cd /opt ; git clone https://github.com/makhomed/nftables-tool.git
```

## Upgrade
```
python -m pip install --no-input --upgrade-strategy eager --upgrade Jinja2 requests invoke ; \
cd /opt/nftables-tool ; git pull
```

## Usage
```
/opt/nftables-tool/nftables-tool
```
or
```
/opt/nftables-tool/nftables-tool 172.21.0.0/16 2001:DB8:11:22::/64 2001:DB8:99:77::/64
```

## Automation via cron

Configure cron job, for example, in file `/etc/cron.d/nftables-tool`:

```
RANDOM_DELAY=360

0 0 * * * root /opt/nftables-tool/nftables-tool
```
or
```
RANDOM_DELAY=360

0 0 * * * root /opt/nftables-tool/nftables-tool 172.21.0.0/16 2001:DB8:1:2::/64 2001:DB8:8:9::/64
```

## TODO

- Update [`contrib/nftables.conf`](https://github.com/makhomed/nftables-tool/blob/master/contrib/nftables.conf) using recommendations
  from [RFC 4890](https://datatracker.ietf.org/doc/html/rfc4890) and related documents for IPv4 ICMP filtering.

