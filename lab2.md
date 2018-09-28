# Notes for solution to lab 2

Handy resources: 

* <https://www.cisco.com/c/en/us/td/docs/wireless/access_point/15-3-3/configuration/guide/cg15-3-3/cg15-3-3-chap4-first.html#39486>
* <https://www.cisco.com/c/en/us/support/docs/wireless/aironet-1100-series/46141-vlanswireless.html#brg>

## Task 4

* "Disabled DSSS speeds" by setting ´speed basic-12.0´
* Why is it common to disable DSSS speeds? Because instead of providing bad speeds at far distances, it might be better to not provide service there at all, to force the client to find a new (better) AP.
* bridge-group: has to do with how the AP handles broadcasts. I think broadcasts are only relayed on interfaces in the same bridge-group

## Task 5

* Wireshark: TBD
