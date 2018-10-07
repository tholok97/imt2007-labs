# Lab 3 notes

## Task 2

**Dialog during initial configuration of WLC**:

```
System Name [Cisco_6f:6d:24] (31 characters max):
Enter Administrative User Name (24 characters max): admin
Enter Administrative Password (3 to 24 characters): ******* ! (Thomas kommentar: NTNUiG1)
Re-enter Administrative Password                 : *******  ! (Thomas kommentar: NTNUiG1)

Enable Link Aggregation (LAG) [yes][NO]: NO

Management Interface IP Address:
Invalid response


Management Interface IP Address:
Invalid response


Management Interface IP Address: 192.168.11.10
Management Interface Netmask: 255.255.255.0
Management Interface Default Router: 192.168.11.1
Cleaning up Provisioning SSID
Management Interface VLAN Identifier (0 = untagged): 0
Management Interface Port Num [1 to 4]: 1
Management Interface DHCP Server IP Address: 192.168.11.1

Virtual Gateway IP Address: 192.168.255.254

Multicast IP Address: 239.0.1.1

Mobility/RF Group Name: mobility_group_1

Network Name (SSID):
Invalid response


Network Name (SSID): none

Configure DHCP Bridging Mode [yes][NO]: no

Allow Static IP Addresses [YES][no]: yes

Configure a RADIUS Server now? [YES][no]: no
Warning! The default WLAN security policy requires a RADIUS server.
Please see documentation for more details.

Enter Country Code list (enter 'help' for a list of countries) [US]: NO

Enable 802.11b Network [YES][no]: yes
Enable 802.11a Network [YES][no]: yes
Enable 802.11g Network [YES][no]: yes
Enable Auto-RF [YES][no]: yes

Configure a NTP server now? [YES][no]: 129.241.0.123
Invalid response


Configure a NTP server now? [YES][no]: yes
Enter the NTP server's IP address: 129.241.0.123
Enter a polling interval between 3600 and 604800 secs: 10000

Would you like to configure IPv6 parameters[YES][no]: no

Configuration correct? If yes, system will save it and reset. [yes][NO]: yes
 Cleaning up DHCP Server
Cleaning up Provisioning SSIDRestoring web auth certRestoring web auth cert

Configuration saved!
Resetting system with new configuration...


Configuration saved!
Resetting system with new configuration...
Creating license client restartability thread
Restarting system.
```

* Put management interface of WLC on VLAN 11 initially. This was wrong, should be untagged, as switch port has native VLAN as 11, so untagged frames are handled as 11 anyway.
* Couldn't connect to website initially. It was turned off. Had to do `config network webmode enable`
* PSK "key" (?): VERYSECRETPSK
* For uploading the file from the controller to my computer via tftpd64, path "/" had to be used.
* Uploaded two files for wlc config. `config.cisco` is the file taken straight from the wlc. `lab3_wlc_config.cisco` is the same file, but copy-pasted. Github gave a warning about line-endings, so I'm leaving the config.cisco file in for now in case the other one doesn't work.

## Task 3

* Did not manage to upload the `task3_wlc_config.cisco` file to the WLC...
* REMEMBER TO MAKE SURE THE TIME IS CORRECT ON THE WLC!!
* Had lots of problems with second part of this task. The second AP refused to connect to the WLC. When using an identical setup, and plugging in the second AP instead, it all worked fine. I'm suspecting there's an issue with the second AP, so I've decided to give up and retry later on a another pod. Some facts:
    * They seem to be the same model and version
    * I've fixed the clock on both controller and AP, but that didn't help
    * I've browsed solutions to similar issues. One had to do with licensing, the other had to do with NTP. None helped, although I did not explore the licensing solution too much.
* **Solution to above problem**:
    * Reason one AP worked and one didn't: Because the one that worked had the WLC management IP address stored from connecting to it on a vlan 11 port. Once this IP was deleted both APs had the same issue.
    * The problem was that I wrote the option 43 IP address in the wrong format. I wrote `option 43 ascii "192.168.11.10`, but the AP was expecting `option 43 hex f104C0A80B0A`. 
    * [Link to where I found the solution](https://www.cisco.com/c/en/us/support/docs/wireless-mobility/wireless-lan-wlan/97066-dhcp-option-43-00.html#anc9)
* To make router relay WLC discovery broadcasts to controller across VLANs:

        ip forward-protocol udp 5246
        int g0/1.22
            ip helper-address 192.168.11.10
            
* Note: An AP connected directly to the WLC on a PoE port gets assigned an address in VLAN 11, and can successfully connect to the WLC.

## Task 4

* Did all of it in the GUI. Googling each specific task led me in the right direction.
* Not sure if I managed to setup enforcing OFDM modulation..
