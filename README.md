# BitMS Software | Developer Configuration

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

**STEP 3 «create a certificate for a personal domain name»**

```
    $ echo "127.0.0.1  example.local" >> /etc/hosts
    $ mkdir -p /etc/nginx/ssl/example.local
```


**STEP 3.1 «create the file for X.509 v3»**
```
    $ sudo nano /etc/nginx/ssl/example.local/x509v3.ext
```

**STEP 3.2 «write context for X.509 v3»**

_**example.local** - This is a custom local domain name._ 
```
authorityKeyIdentifier = keyid, issuer
basicConstraints = CA: FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names
[alt_names]
DNS.1 = example.local
```

**STEP 3.3 «create private key and signature»**

```
    $ sudo openssl req -new -nodes -out /etc/nginx/ssl/example.local/certificate.csr \ 
      -newkey rsa:2048 -keyout /etc/nginx/ssl/example.local/private.key
```

**STEP 3.4 «create private key and signature»**

```
    $ sudo openssl x509 -req -in /etc/nginx/ssl/example.local/certificate.csr \
      -CA /etc/nginx/ssl/localhostCA.pem -CAkey /etc/nginx/ssl/localhostCA.key \
      -CAcreateserial -out /etc/nginx/ssl/example.local/certificate.crt \
      -days 500 -sha256 -extfile /etc/nginx/ssl/example.local/x509v3.ext
```

**STEP 4 «add private key and certificate in the nginx»**

```
    $ sudo nano /etc/nginx/config.d/exmaple.conf
```

_configuration nginx_
```
server {

    #
    #   Install 443 port and http2 - this is Nginx module
    #
    listen 443 ssl http2;

    server_name example.local;

    #
    #   Nginx module settings
    #
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_ciphers "EECDH+ECDSA+AESGCM:EECDH+aRSA+AESGCM:EECDH+ECDSA+SHA256:EECDH+aRSA+SHA256:EECDH+ECDSA+SHA384:EECDH+ECDSA+SHA256:EECDH+aRSA+SHA384:EDH+aRSA+AESGCM:EDH+aRSA+SHA256:EDH+aRSA:EECDH:!aNULL:!eNULL:!MEDIUM:!LOW:!3DES:!MD5:!EXP:!PSK:!SRP:!DSS:!RC4:!SEED";

    #
    #   Include file private key and certificate
    #
    ssl_certificate /etc/nginx/ssl/example.local/certificate.crt;
    ssl_certificate_key /etc/nginx/ssl/example.local/private.key;

    root /var/www/example/html;

    index index.php index.html;


    # ... add other nginx configuration
}
```
**If redirect**
```
#
#   Append /etc/nginx/config.d/example.conf
#
server {
    #
    # Default port
    #
    listen 80;
    listen [::]:80;

    charset utf8;
    
    error_log /var/log/nginx/80-error.log;

    server_name example.local;

    if ($host = example.local) {
        return 301 https://$host$request_uri;
    }

}
```

**Nginx reload, init new configuration**
```
    $ systemctl restart nginx.service
```

**STEP 6 «add a certificate for the browser»**

Add Google Chrome / Chromium [chrome://settings/certificates](chrome://settings/certificates)