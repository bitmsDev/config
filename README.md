# BitMS Software | Developer Configuration

> Nginx configuration 

```
#
#  HTTP2/TSL
#
server {
    
}

#
#  DEFAULT :80
#
server {

}
```

> Location SSL

**STEP 1 «create private key»**
```
    $ mkdir -p /etc/nginx/ssl/
    $ sudo openssl genrsa -des3 -out /etc/nginx/ssl/localhostCA.key 2048
```

**STEP 2 «create root certificate»**
```
    $ sudo openssl req -x509 -new -nodes -key /etc/nginx/ssl/localhostCA.key \
      -sha256 -days 1024 -out /etc/nginx/ssl/localhostCA.pem
```

**STEP 3 «create the file for X.509 v3»**
```
    $ sudo nano /etc/nginx/ssl/x509v3.ext
```

**STEP 3.1 «write context for X.509 v3»**

_**mydomains.local** - This is a custom local domain name._ 

```
authorityKeyIdentifier = keyid, issuer
basicConstraints = CA: FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names
[alt_names]
DNS.1 = mydomains.local
```

