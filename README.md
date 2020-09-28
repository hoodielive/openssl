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
Make sure that you don't leave out *'-pubout'* as the point will be neglected.

**Create an ECDSA key with secp256r1 Named Curve:**
```bash
openssl ecparam -genkey -name secp256r1 | openssl -out ec.key -aes128
```

**Create a CSR from key:**
```bash
openssl req -new -key fd.key -out fd.csr
```

**Inspect the CSR:**
```bash
openssl req -text -in fd.csr -noout
```

**Create CSR(s) for Existing Certificates:**
```bash
openssl x509 -x509toreq -in fd.crt -out fd.csr -signkey fd.key
```

**Unattend CSR Generation:**
First create a fd.cnf file with something akin to the following content:
```
[req]
prompt = no
distinguished_name = distinguished_name

[distinguished_name]
CN = poc.rhce.lab
emailAddress = rhce@poc.rhce.lab
O = Proof of Concept
L = Pennsylvania
C = Pittsburgh
```
```bash
openssl req -new -config fd.cnf -key fd.key -out fd.csr
```

**Sign your Certificates:**
```bash
openssl x509 -req -days 365 -in fd.csr -signkey fd.key -out fd.crt
```

**Troubleshooting the following error:**
```
140208884414272:error:0D07A097:asn1 encoding routines:ASN1_mbstring_ncopy:string too long:crypto/asn1/a_mbstr.c:107:maxsize=2
```
This means, that your 'C' (country) should be '2' Letters only.
