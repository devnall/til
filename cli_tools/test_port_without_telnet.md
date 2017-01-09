# Test connectivity to a port when you don't have telnet installed

If you don’t have telnet installed (say, in a docker) and want to test connectivity to a port on a remote system:
`(echo > /dev/tcp/$hostname/$port) >/dev/null 2>&1 && echo "Up" || echo "Down"`
to return Up if it can connect and Down if it can't
