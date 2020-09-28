#### Lets Study OpenSSL:

**Create a private key | encrypted:**
```bash
openssl genrsa -aes128 -out fd.key 2048
```

**Note:** This command prompts for a password. Do not forget password or you will not be able to 'decrypt' said key for whatever reason.

**Inspect the key by using the following command:**
```bash
openssl rsa -text -in fd.key 
```

**Perform a transform from 'private encrypted' to 'public':**
```bash
openssl rsa -in fd.key -pubout -out fd-public.key
```
*Make sure that you don't leave out '-pubout' as the point will be neglected.*

**Create an ECDSA key with secp256r1 Named Curve:**
```bash
openssl ecparam -genkey -name secp256r1 | openssl -out ec.key -aes128
```
