# Arista and Juniper Carrier-Supporting-Carrier VPN 

In this scenario we have Two Service Providers, Provider A is using Arista with ASN 65001 and Provider B is using Juniper with ASN 65002.

![CSC VPN](/csc-vpn.png)
---
Provider A wants to offer MPLS services, but it needs to cross through Provider B. To make this solution work Service Providers need to peer using Labeled-Unicast. This way Service Provider B can carry MPLS traffic for Service Provider A.


Another interesting challenge is this will create a BGP ASN routing loop so Service Provider B will need to override the AS-PATH.

Using EVPN we peer from PE-1 to RR-1 which will peer with RR-2. RR-2 peers with PE-2 and using route-reflectors we can carry EVPN advertisements across Service Provider B PE to PE.

To make this solution fully work route reflectors must NOT change the next-hop address in BGP so PE sees the advertisement from the other PE.

Then we use EVPN Type-5 Route to provide L3VPN service to Customer Blue and EVPN Type-2 Route to provide L2VPN service to Customer Green.

