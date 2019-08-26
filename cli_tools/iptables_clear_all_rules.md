# Clearing All iptables Rules

This clears all existing iptables rules and get it back to a fresh state:

```
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -t nat -F
iptables -t mangle -F
iptables -F
iptables -X
```

Clear ip6tables rules:
```
ip6tables -P INPUT ACCEPT
ip6tables -P FORWARD ACCEPT
ip6tables -P OUTPUT ACCEPT
ip6tables -t nat -F
ip6tables -t mangle -F
ip6tables -F
ip6tables -X
```

Verify that no rules still exist via `iptables -nvL`

Source:
https://serverfault.com/questions/200635/best-way-to-clear-all-iptables-rules
