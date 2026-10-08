# Task 4 — Run a Different HTML Page on a Separate Port

## Objective
Create a second HTML page and serve it from Nginx on a different port.

## Second Web Root

The second document root is:

```text
/var/www/second_page
```

The HTML file contains:

```html
<h1>This is the second HTML page run on a different port</h1>
```

## Nginx Configuration

A separate site configuration was created at:

```text
/etc/nginx/sites-available/second_page
```

Configuration:

```nginx
server {
    listen 8002;
    root /var/www/second_page;
    index index.html;
}
```

The site was enabled with:

```bash
sudo ln -sf /etc/nginx/sites-available/second_page \
/etc/nginx/sites-enabled/second_page
```

## Configuration Test

```bash
sudo nginx -t
```

The evidence shows:

```text
syntax is ok
test is successful
```

Then Nginx was restarted:

```bash
sudo systemctl restart nginx
```

## Verification

The final verification was performed with:

```bash
curl 10.10.145.207:8002
```

The successful response was:

```html
<h1>This is the second HTML page run on a different port</h1>
```

The terminal also shows earlier `404 Not Found` responses while the second page was being prepared. This was resolved after creating the correct document root and `index.html`.

## Result
Task 4 was successfully implemented: the second HTML page is served independently through Nginx on TCP port `8002`.

## Evidence
Five screenshots are included in `evidence/task-4-second-port/`.

## Organizer Demonstration
Run:

```bash
curl http://10.10.145.207:8002
```

and show the returned second-page heading.
