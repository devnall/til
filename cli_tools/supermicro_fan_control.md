# Changing Fan Settings on Supermicro Systems

## Problem:
Supermicro systems are freaking loud. No big deal in a datacenter, very big deal in a home lab.

## Solution

There are 3 different fan modes. To view the current mode:
`ipmitool raw 0x30 0x45 0x00`
which will output an `0x0#` where `#` is one of:
`0` = standard fan mode
`1` = full fan mode
`2` = optimal fan mode
`4` = heavy I/O fan mode

To change to a different fan mode:
`ipmitool raw 0x30 0x45 0x01 0x0#`
replacing the `#` with one of the options above.

You can keep an eye on temperatures after the change via:
`ipmitool sensor`

Generally speaking, "Optimal" should be fine for a home server that won't be under crazy load. Standard is noisier and cooler if needed. More info in links below.

## References:
* https://forums.servethehome.com/index.php?resources/supermicro-x9-x10-x11-fan-speed-control.20/
* https://www.supermicro.com/support/faqs/faq.cfm?faq=18025
* https://forums.servethehome.com/index.php?threads/supermicro-x9-x10-x11-fan-speed-control.10059/
