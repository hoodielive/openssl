# Lets Study OpenSSL:

Study OpenSSL

Create a private key | encrypted:
```bash
openssl genrsa -aes128 -out fd.key 2048
```

Inspect the key by using the following command: 
```bash
openssl rsa -text -in fd.key 
```
