# How to Flush DNS Cache in MacOS

## 10.11 and newer, 10.8, 10.7

`sudo killall -HUP mDNSResponder`

## 10.10 Yosemite

`sudo discoveryutil mdnsflushcache && sudo discoveryutil udnsflushcaches`

## 10.9 Mavericks

`dscacheutil -flushcache && sudo killall -HUP mDNSResponder`
