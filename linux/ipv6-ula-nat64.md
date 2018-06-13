# IPv6 Unique Local Addresses and NAT64 on Linux
Today I was installing lxd on a fresh virtual machine. lxd init asked if
I'd like to have an IPv6 subnet configured automatically. So I accepted and
it generated subnet fd42:7ced:99d6:7b31::/64 and attached it to the lxd bridge.

This was quite a revelation for me, as I didn't even know "private prefixes"
existed for IPv6 in the first place.
This turned out to be generated in the [Unique Local Address](https://en.wikipedia.org/wiki/Unique_local_address) (ULA) prefix fd00::/8.
The actual ULA prefix is fc00::/7, but apparently only the last /8 is being
used.

Anyway, I launched a test container in lxd and to my pleasant surprise lxd
had already added ip6tables to be able to use NAT64, which is the IPv6
equivalent of IPv4 NAT. This allows containers to speak to the public IPv6 network, while being unreachable from the outside.

For later reference, this is the commands to actually enable NAT64:
```bash
ip6tables -t nat -A POSTROUTING -s fd42:7ced:99d6:7b31::/64 \! -d fd42:7ced:99d6:7b31::/64 -j MASQUERADE
```

Obviously replace fd42:7ced:99d6:7b31::/64 with your own local ULA prefix.
