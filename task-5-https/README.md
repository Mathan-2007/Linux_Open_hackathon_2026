# Task 5 — Convert the Hosted Page to HTTPS

## Objective
Serve the custom HTML page through HTTPS using Nginx.

## Certificate Generation

A self-signed RSA certificate was generated with OpenSSL:

```bash
sudo openssl req -x509 -nodes -days 365 \
-newkey rsa:2048 \
-keyout /etc/ssl/private/nginx-selfsigned.key \
-out /etc/ssl/certs/nginx-selfsigned.crt
```

Certificate subject information was entered during the OpenSSL prompts.

## Nginx HTTPS Configuration

The Nginx default server configuration was edited to enable SSL on port `443`.

The relevant configuration concept is:

```nginx
listen 443 ssl default_server;
listen [::]:443 ssl default_server;
```

and the server uses the generated certificate and private key.

## Configuration Validation

```bash
sudo nginx -t
```

The evidence shows:

```text
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

Nginx was then restarted:

```bash
sudo systemctl restart nginx
```

## HTTPS Verification

Because the certificate is self-signed, normal certificate validation will reject it as untrusted.

For local verification:

```bash
curl -k https://10.10.145.207
```

The `-k` option tells curl to continue despite the self-signed certificate.

The HTTPS request returned the custom HTML page, confirming that the page was being served over TLS.

## Security Note

This certificate is appropriate for a local hackathon/lab demonstration. It is **not a trusted production certificate**.

For a production deployment, use a certificate issued by a trusted CA and configure a proper hostname.

## Result
HTTPS was configured and the custom page was successfully returned through the HTTPS endpoint.

## Evidence
Five screenshots are included in `evidence/task-5-https/`.

## Organizer Demonstration

Run:

```bash
curl -k https://10.10.145.207
```

Then open:

```text
https://10.10.145.207
```

in a browser and explain that the browser warning is expected because the certificate is self-signed.
