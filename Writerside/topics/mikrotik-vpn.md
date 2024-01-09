# VPN-тунель между микротиками

**Server:**

```bash
# jan/02/1970 00:41:37 by RouterOS 6.48.6
# software id = JYWH-BL77
#
# model = 960PGS
# serial number = AD8A097C5A3A
/interface bridge
add name=bridge1
/interface eoip
add local-address=172.16.0.1 mac-address=02:CE:52:09:78:D4 name=eoip-tunnel1 \
    remote-address=172.16.0.2 tunnel-id=1
/interface wireless security-profiles
set [ find default=yes ] supplicant-identity=MikroTik
/ip hotspot profile
set [ find default=yes ] html-directory=hotspot
/ip pool
add name=dhcp_pool0 ranges=192.168.1.100-192.168.1.200
/ip dhcp-server
add address-pool=dhcp_pool0 disabled=no interface=bridge1 name=dhcp1
/ppp profile
set *FFFFFFFE use-compression=no use-encryption=no
/interface bridge port
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=ether3
add bridge=bridge1 interface=ether4
add bridge=bridge1 interface=ether5
add bridge=bridge1 interface=eoip-tunnel1
/interface l2tp-server server
set enabled=yes ipsec-secret=1
/ip address
add address=10.0.0.1/24 interface=ether1 network=10.0.0.0
add address=192.168.1.1/24 interface=bridge1 network=192.168.1.0
/ip dhcp-server network
add address=192.168.1.0/24 gateway=192.168.1.1
/ppp secret
add local-address=172.16.0.1 name=user1 password=1 remote-address=172.16.0.2 \
    service=l2tp
```

**Client:**

```bash
# jan/02/1970 00:43:31 by RouterOS 6.42.7
# software id = 8XTR-N1H4
#
# model = 960PGS
# serial number = AD8A09866FDF
/interface bridge
add fast-forward=no name=bridge1
/interface l2tp-client
add connect-to=10.0.0.1 disabled=no ipsec-secret=1 name=l2tp-out1 password=1 \
    user=user1
/interface eoip
add local-address=172.16.0.2 mac-address=02:12:BB:3D:61:11 name=eoip-tunnel1 \
    remote-address=172.16.0.1 tunnel-id=1
/interface wireless security-profiles
set [ find default=yes ] supplicant-identity=MikroTik
/ppp profile
set *FFFFFFFE use-compression=no use-encryption=no
/interface bridge port
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=ether3
add bridge=bridge1 interface=ether4
add bridge=bridge1 interface=ether5
add bridge=bridge1 interface=eoip-tunnel1
/ip address
add address=10.0.0.2/24 interface=ether1 network=10.0.0.0
add address=192.168.1.2/24 interface=bridge1 network=192.168.1.0
/system routerboard settings
set silent-boot=no
```