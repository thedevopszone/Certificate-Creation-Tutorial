# Certificate Creation Tutorial

## Steps To Create A Certifikate

1) Generate a private key
   
```
openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -pkeyopt rsa_keygen_pubexp:3 -out privkey-A.pem
```

2) Generate a public key
   
```
openssl pkey -in privkey-A.pem -pubout -out pubkey-A.pem
```

Aside:
```
# Viewing the keys in plain text
openssl pkey -in privkey-A.pem -text -noout
openssl pkey -pubin -in pubkey-A.pem -text -noout
```

3) Generate a certificate signing request
   
```
openssl req -new -key privkey-A.pem -out A-req.csr

The command will prompt Alice with these questions:
● Country code [C]: {Alice fills in her country code}
● Province/STate name [ST]: {Alice fills in her province name fully}
● City/Location [L]: {The city Alice’s business is registered in, for example}
● Organization Name [O]: {Alice’s business name, for example}
● Organizational Unit Name [OU]: (Optional) {What part of the company is she?}
● Common Name [CN]: the hostname+domain, i.e. “www.alice.com”
● A challenge password []: {this can be used as a secret nonce between Alice and CA}
```

Aside: generating a self-signed certificate for the CA
```
openssl req -x509 -new -nodes -key rootkey.pem -sha256 -days 1024 -out root.crt
```



