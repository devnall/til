# OpenSSL: How to verify that a cert and a key go together

The private key contains a series of numbers. Two of those numbers form the "public key", the others are part of your "private key". The "public key" bits are also embedded in your Certificate (we get them from your CSR). 

To check that the public key in your cert matches the public portion of your private key, you need to view the cert and the key and compare the numbers.

To view the certificate and the key, run the commands:
`openssl x509 -noout -text -in server.crt`
`openssl rsa -noout -text -in server.key`

The "modulus" and the "public exponent" portions in the key and the cert must match.


Since the public exponent is usually 65537 and it's a pain to compare the long modulus, you can use the following approach:

`openssl x509 -noout -modulus -in server.crt | openssl md5`
`openssl rsa -noout -modulus -in server.key | openssl md5`

...and then compare these shorter numbers. With overwhelming probability, they will differ if the keys are different.


As a "one-liner":
`openssl x509 -noout -modulus -in server.pem | openssl md5 ;\
openssl rsa -noout -modulus -in server.key | openssl md5`


And with auto-comparison (if more than one hash is displayed in the output, the key and cert *don't* match):

`(openssl x509 -noout -modulus -in server.pem | openssl md5 ;\
openssl rsa -noout -modulus -in server.key | openssl md5) | uniq`


As an aside, if you want to check which key or cert a particular CSR belongs to, you can get the CSR hash to compare via:
`openssl req -noout -modulus -in server.csr | openssl md5`
