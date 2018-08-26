# Lab 1

## VLANs

(First 10 addresses are excluded from dhcp, meant for static. (1-10))

|id|name        |subnet             |num. addr. |
|--|------------|-------------------|-----------|
|11|Management  |192.168.11.0/24    | 254       |
|12|Staff       |192.168.12.0/24    | 254       |
|13|Guests      |192.168.13.0/24    | 254       |
|21|AP1         |192.168.21.0/24    | 254       |
|22|AP2         |192.168.22.0/24    | 254       |

## Devices

(Each VLAN has a sub-interface on g0/1 on the router, and this sub-interface is assigned the first address in the subnet)

* switch0: 192.168.11.2/18

## Notes

* Cables

    Straight-through: host to client
    Crossover: host to host

    But modern hardware doesn't need this distinction. Straight-through for everything is now standard.

* VTP: VLAN Trunking Protocol
* Native VLAN: What VLAN to treat untagged frame as
* Each physical switch port belongs to a VLAN
* Delete switch config (DOESN'T AFFECT VLAN INFO): `erase startup-config` and then`reload`
* Delete switch VLAN info: 
        dir flash:
        // finn vlan.dat
        delete flash:vlan.dat
        reload
* `show interface brief`
* `show interface trunk`
* stop command from running: shift+6
* Router-on-a-stick:
    - Phyical interface on router end needs to be no shut
    - Interface on switch end needs to be in trunking mode
* Netacad module 3 chapter 5 has lots of info.
* To verify dhcp: `show ip dhcp binding`
* DHCPv4 Relay: When router receives dhcp broadcast discover, but isn't a DHCP server itself, it can relay the request as a unicast towards DHCP server it knows about.
* Lab "10.1.2.5 Lab - Configuring Basic DHCPv4 on a Switch" might be worth doing.
* Private IPv4 Adresses:
    - 10.0.0.0/8
    - 172.16.0.0/12
    - 192.168.0.0/16
* NAT:
    - Inside network: set of networks that is subject to translation
    - Outside network: all other networks
    - Local address: an address that appears on the inside portion of the network
    - Global address an address that appears on the outside portion of the network
    - Types:
        * Static NAT (one-to-one)
        * Dynamic NAT (many-to-many)
        * Port Address Translation (NAT overloading) (many-to-one)
            - Uses TCP port number to distinguish different machines
            - Tries to preserve port number, but uses next available one if port number taken
    - NAT doesn't allow incomming connections. Port forwarding is a way to make it do that as well.
    - NAT is used to provide access between IPv4 and IPv6 networks, but other than that IPv6 doesn't need NAT
* Port security: limit what MAC-addresses can communicate through physical interface (port)

##  Questions

* How to simulate internet-connection?
* What is (on router) "%Error opening tftp://10.10.0.8/network-config (Timed out)
* **Inside local, outside global (, ...) NAT terminology is confusing..**
