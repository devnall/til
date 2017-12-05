# How to verify that a TLS/SSL key matches a given cert

In the event that you have a .crt file and a .key file and want to verify that they go together:

```
openssl-modulus-key () {
    openssl rsa -noout -modulus -in "$1" | openssl md5
}
openssl-modulus-crt () {
    openssl x509 -noout -modulus -in "$1" | openssl md5
}
```

As long as the hashes match, you should be all set.
