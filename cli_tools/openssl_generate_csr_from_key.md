# OpenSSL: HowTo Generate a New CSR From an Existing Key

Most people, even beardy Ops grognards who should know better, seem to
generate a new CSR and key every time they need to renew an SSL/TLS cert.

As long as you have the .key, you can generate a new CSR from that key, which
will give you one fewer thing to update and one fewer thing that could
potentially break.

Assuming `my_domain_name.key` is your keyfile:
`openssl req -out my_domain_name.csr -key my_domain_name.key -new`

Then just submit that new CSR to your registrar, get the new CRT back, and
replace the old CRT with the new one; no need to change the key!
