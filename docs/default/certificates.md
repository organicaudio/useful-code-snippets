# Certificates and encryption

## file types

- .pem: 
    - contains as first line: `-----BEGIN CERTIFICATE-----`
    - can be a private key or a public certificate
    - can be read with text editor but is base64 encoded
    - or with: `openssl x509 -in cert.pem -text`
- .der (.cer) binary encoded x509 certificate
- .key private key in PEM format
- .cert;.cer;.crt: certificate with private key (DER or PEM)
- .p12 - pkcs12 container which contains private key and public certificate
- .pfx - pkcs12
- .csr (certificate signing request): temporary 

## generate (self signed)

### certificate and private key in pem format

```shell
# create 
## with subject prompt
openssl req -x509 -newkey rsa:4096 -keyout my.key -out my.crt -days 365
## without subject prompt
openssl req -x509 -newkey rsa:4096 -keyout my.key -out my.crt -days 365 -subj /CN=example.de

# read 
openssl x509 -in  my.crt -text -noout
openssl rsa -in my.crt -text -noout
```

### Java truststore and keystore

- A Java keystore holds your private Keys + and your certificate
- A Java truststore holds the certificates you trust when you connect yourself to a server   
- You may need to assure that the truststore contains the whole trust-chain otherwise java may not accept a connection to the server  
- .fileending (Format): .jks (JSK), .keystore (JSK), .p12 (PKCS12)
- pkcs12 is the recommended format for keystores, not jks
- Javas bundled truststore resides in `$JAVA_HOME/jre/lib/security/jssecacerts` and `$JAVA_HOME/jre/lib/security/cacerts`
- java Properties 
  - `javax.net.ssl.keyStore*` 
  - `javax.net.ssl.trustStore*` 
  - `javax.net.debug` to activate debugging
  - `javax.net.ssl.*trust*StoreType` from java 9 onwards keyStoreType is pkcs12. Before it was jks.

```shell
# assumes that .crt and .key already exist

## 1. create pem with full chain of trust
cat  my.crt > full-chain.crt

## 2. create Keystore in .p12 format from .key and .crt. To pass prompt use -passin -passout
### you may want to set keystorepassword=privatekeypassword because some libraries assume that
openssl pkcs12 -export -in full-chain.crt -inkey my.key -out keystore.p12

## 3. create Truststore (add .crt) - which trust the cert and use changeit as password for the truststore
openssl pkcs12 -export -nokeys -in full-chain.crt -out truststore.p12

## (not recommended) keystore as jks. convert p12 to jks
keytool -importkeystore -srckeystore keystore.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -deststoretype jks

## (not recommended) truststore as jks 
keytool -keystore truststore.jks -alias full-chain.crt -import -file full-chain.crt -noprompt -storepass changeit
```

### ssh key

To generate ssh keys run `ssh-keygen` which generates ~/.ssh/id_rsa.pub and ~/.ssh/id_rsa. The private and public key do no use the pem format. The name of the owner is at the end of the pub file.

### x.509 certificates

Fields:

- common name (cn):
- 

## tools

### mkcert

[mkcert](https://github.com/FiloSottile/mkcert)

### vscode opensslutils

[opensslutils](https://marketplace.visualstudio.com/items?itemName=ffaraone.opensslutils)