# OpenHack Nginx Web Server — Complete Task Documentation

## Participant
- **Name:** MATHAN S
- **Environment:** Kali Linux
- **Primary server IP:** `10.10.145.207`
- **Primary interface:** `wlan0`
- **Primary HTTP service:** Nginx
- **Second HTTP service:** Nginx on port `8002`
- **HTTPS:** Nginx with a self-signed certificate

## Competition Tasks

This repository documents the five required tasks in the exact order specified by the organizers:

1. Set up Nginx and serve the organizer-provided custom HTML page.
2. Access the hosted page from another computer on the same network.
3. Modify the custom HTML page from another computer and verify the change.
4. Run a different HTML page on a separate port and verify access.
5. Convert the hosted page to HTTPS and verify secure access.

## Important Evidence Note

The supplied screenshots document the terminal configuration and verification work. Some screenshots demonstrate supporting steps rather than the final scoring condition itself.

In particular:
- The screenshots show the server IP, Nginx status, SSH service, HTTP responses, and the second port.
- For Tasks 2 and 3, the final competition demonstration should be performed from a **separate physical computer** on the same network. A local terminal or an SSH session alone should not be presented as proof of a separate physical machine.
- Task 5 uses a **self-signed certificate**. Therefore a normal browser will warn that the certificate is not trusted. `curl -k` is used only to verify that the HTTPS endpoint is serving the page.

## Evidence Layout

Each task contains exactly five screenshots:

- `evidence/task-1-nginx/`
- `evidence/task-2-remote-access/`
- `evidence/task-3-remote-modification/`
- `evidence/task-4-second-port/`
- `evidence/task-5-https/`

## Final Demonstration Checklist

### Task 1
```bash
sudo nginx -t
sudo systemctl status nginx
curl http://10.10.145.207
```

Expected result: Nginx is running and the organizer's custom HTML is returned.

### Task 2
From a second computer:
```bash
curl http://10.10.145.207
```
or open:
```text
http://10.10.145.207
```

Expected result: the custom page loads from the second computer.

### Task 3
From the second computer, connect to the server using the permitted remote method, edit the HTML file, then verify:
```bash
curl http://10.10.145.207
```

Expected result: the changed text is returned without restarting Nginx.

### Task 4
Verify:
```bash
curl http://10.10.145.207:8002
```

Expected result:
```html
<h1>This is the second HTML page run on a different port</h1>
```

### Task 5
Verify:
```bash
curl -k https://10.10.145.207
```

Expected result: the same custom page is returned over HTTPS.

## Main Configuration

Primary web root:
```text
/var/www/html
```

Second web root:
```text
/var/www/second_page
```

Second Nginx server:
```nginx
server {
    listen 8002;
    root /var/www/second_page;
    index index.html;
}
```

## HTTPS Certificate

A self-signed certificate was generated with OpenSSL. The certificate and key were placed under:
```text
/etc/ssl/certs/
 /etc/ssl/private/
```

The certificate is intended for a local demonstration environment, not production use.

## GitHub Submission

The repository should contain:
- This README.
- Five task-specific Markdown files.
- Exactly five evidence screenshots per task.
- The Nginx configuration used for the second port.
- Any final HTML files that are safe and appropriate to submit.
