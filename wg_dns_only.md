# Changes in the .conf files for wireguard

The wireguard script from https://github.com/Nyr/wireguard-install routes the whole traffic. Just look at the .conf files:

```
[Interface]
Address = 10.7.0.5/24
DNS = 192.168.178.22  # <- this is the PiHole
PrivateKey = fiuhrefiuwfhl...

[Peer]
PublicKey = +hasdasdasd...
PresharedKey = adasdasdaf...
AllowedIPs = 0.0.0.0/0, ::/0
Endpoint = dyndns.provider.com:51280
PersistentKeepalive = 25
```

If a PiHole is running in your network, e.g. IP 192.168.178.22, the .conf can be changed like this:

```
[Peer]
PublicKey = +hasdasdasd...
PresharedKey = adasdasdaf...
AllowedIPs = 10.7.0.0/24, 192.168.178.0/24
Endpoint = dyndns.provider.com:51280
PersistentKeepalive = 25
```

In this case the routers IP is 192.168.178.1 (Fritz!Box, e.g.).

Only the DNS traffic will be routed through the wireguard connection and all other traffic through
your "normal" Internet-Access.
