# VPN-сервер на микротике

```bash
/interface bridge
add admin-mac=64:D1:54:83:06:45 auto-mac=no comment=defconf igmp-snooping=yes name=bridge
/interface list
add comment=defconf name=WAN
add comment=defconf name=LAN
/interface wireless security-profiles
set [ find default=yes ] supplicant-identity=Router
/ip pool
add name=default-dhcp ranges=192.168.69.20-192.168.69.254
add name=vpn_pool ranges=192.168.100.1-192.168.100.254
/ip dhcp-server
add address-pool=default-dhcp disabled=no interface=bridge lease-time=1h name=defconf
/port
set 0 name=serial0
/ppp profile
add change-tcp-mss=yes local-address=vpn_pool name=vpn remote-address=vpn_pool use-encryption=yes
set *FFFFFFFE local-address=default-dhcp remote-address=default-dhcp
/user group
set full policy=local,telnet,ssh,ftp,reboot,read,write,policy,test,winbox,password,web,sniff,sensitive,api,romon,dude,tikapp
/interface bridge port
add bridge=bridge comment=defconf interface=ether2
add bridge=bridge comment=defconf interface=ether3
add bridge=bridge comment=defconf interface=ether4
add bridge=bridge comment=defconf interface=ether5
/ip neighbor discovery-settings
set discover-interface-list=LAN
/interface l2tp-server server
set authentication=mschap2 default-profile=vpn enabled=yes ipsec-secret=SECRET_KEY use-ipsec=required
/interface list member
add comment=defconf interface=bridge list=LAN
add comment=defconf interface=ether1 list=WAN
/interface pptp-server server
set default-profile=vpn
/ip address
add address=192.168.69.1/24 comment=defconf interface=bridge network=192.168.69.0
add address=192.168.100.152/24 network=192.168.100.0
/ip dhcp-client
add comment=defconf disabled=no interface=ether1
/ip dhcp-server lease
add address=192.168.69.20 client-id=1:50:3e:aa:12:8:8b comment="COMMENT" mac-address=50:3E:AA:12:08:8B server=defconf
/ip dhcp-server network
add address=192.168.69.0/24 domain=tvhost.ru gateway=192.168.69.1
/ip dns
set allow-remote-requests=yes
/ip dns static
add address=192.168.69.20 comment="COMMENT" regexp=asys
/ip firewall filter
add action=accept chain=input comment="defconf: accept established,related,untracked" connection-state=established,related,untracked
add action=accept chain=forward comment=UDP-TV dst-address=239.255.8.0/21 in-interface-list=WAN protocol=udp
add action=accept chain=input comment=l2tp port=1701,500,4500 protocol=udp
add action=accept chain=input protocol=ipsec-esp
add action=accept chain=input comment="dns for vpn" dst-address=192.168.0.1 dst-port=53 in-interface=all-ppp protocol=udp
add action=drop chain=input comment="defconf: drop invalid" connection-state=invalid
add action=accept chain=input comment="defconf: accept ICMP" protocol=icmp
add action=accept chain=input comment="defconf: accept to local loopback (for CAPsMAN)" dst-address=127.0.0.1
add action=accept chain=input comment=IGMP dst-address=239.255.8.0/21 in-interface-list=WAN protocol=igmp
add action=accept chain=input comment=IGMP-general dst-address=224.0.0.1 in-interface-list=WAN protocol=igmp
add action=drop chain=input comment="defconf: drop all not coming from LAN" in-interface-list=!LAN
add action=accept chain=forward comment="defconf: accept in ipsec policy" ipsec-policy=in,ipsec
add action=accept chain=forward comment="defconf: accept out ipsec policy" ipsec-policy=out,ipsec
add action=fasttrack-connection chain=forward comment="defconf: fasttrack" connection-state=established,related
add action=accept chain=forward comment="defconf: accept established,related, untracked" connection-state=established,related,untracked
add action=drop chain=forward comment="defconf: drop invalid" connection-state=invalid
add action=drop chain=forward comment="defconf: drop all from WAN not DSTNATed" connection-nat-state=!dstnat connection-state=new in-interface-list=WAN
/ip firewall nat
add action=masquerade chain=srcnat comment="defconf: masquerade" ipsec-policy=out,none out-interface-list=WAN
/ip service
set telnet disabled=yes
set ftp disabled=yes
set api disabled=yes
set api-ssl disabled=yes
/ip ssh
set allow-none-crypto=yes forwarding-enabled=local
/ppp secret
add name=VPN_LOGIN password=VPN_PASSWORD profile=vpn service=l2tp
/system clock
set time-zone-name=Europe/Moscow
/tool mac-server
set allowed-interface-list=LAN
/tool mac-server mac-winbox
set allowed-interface-list=LAN
```