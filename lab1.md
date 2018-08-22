# Lab 1

## VLANs

(First 100 addresses are excluded from dhcp, meant for static. (1-100))

|id|name        |subnet             |num. addr. |
|--|------------|-------------------|-----------|
|11|Management  |192.168.0.0/18     |16384      |
|12|Staff       |192.168.64.0/18    |16384      |
|13|Guests      |192.168.128.0/18   |16384      |
|21|AP1         |192.168.192.0/19   |8192       |
|22|AP2         |192.168.224.0/19   |8192       |

## Devices

(Each VLAN has a sub-interface on g0/1 on the router, and this sub-interface is assigned the first address in the subnet)

* switch0: 192.168.0.2/18

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

##  Questions

* How to simulate internet-connection?
* What is (on router) "%Error opening tftp://10.10.0.8/network-config (Timed out)
