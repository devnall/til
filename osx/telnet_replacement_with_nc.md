# Using `nc` as a replacement for `telnet` on MacOS

MacOS doesn't ship with telnet. You can install it with homebrew but sometimes you're on someone else's system or helping someone troubleshoot.

If you just want to know if you can connect to a host:port, you can get that functionality from the netcat (`nc`) command, which _does_ ship with MacOS.

Invoke using hostname or IP:
```
$ nc -vz www.google.com 443
$ nc -vz 64.233.177.99 443
```

Output is pretty self-explanatory:
`Connection to www.google.com port 443 [tcp/https] succeeded!`
`nc: connectx to www.google.com port 443 (tcp) failed: Operation timed out`
`nc: connectx to www.google.com port 443 (tcp) failed: Connection refused`

The options are:
`-v` for more verbose output
`-z` to only scan for listening daemons without sending any data to them
