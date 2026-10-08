# Task 1 — Set Up Nginx and Serve the Custom HTML Page

## Objective
Install/configure Nginx on the local Kali Linux machine and use it to serve the organizer-provided custom HTML page.

## Server Information
- Server IP: `10.10.145.207`
- Web root: `/var/www/html`
- Web server: Nginx
- Default HTTP port: `80`

## Procedure

### 1. Check the Nginx installation and service
The terminal evidence shows Nginx being located and its systemd service being checked.

```bash
which nginx
sudo systemctl status nginx
```

The service output shows the Nginx service running.

### 2. Inspect the web root
```bash
cd /var/www/html
ls
cat index.html
```

The existing default page was inspected before replacing it with the organizer's page.

### 3. Place the custom HTML page in the Nginx document root
The supplied custom HTML was copied into `/var/www/html/index.html`.

The screenshots also document permission problems encountered while changing files under `/var/www/html`. Administrative operations were therefore performed with `sudo`.

### 4. Test Nginx configuration
```bash
sudo nginx -t
```

Expected successful output:
```text
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

### 5. Restart Nginx
```bash
sudo systemctl restart nginx
```

## Result
Nginx was successfully configured and running. The custom HTML page was placed in the Nginx document root and subsequently returned by HTTP requests.

## Evidence
Five screenshots are included in `evidence/task-1-nginx/`.

## Organizer Demonstration
Show:
```bash
sudo systemctl status nginx
curl http://10.10.145.207
```
Then show the returned custom HTML page.
