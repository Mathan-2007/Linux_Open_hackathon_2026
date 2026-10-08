# Task 3 — Modify the HTML Page Remotely and Verify the Change

## Objective
Modify the hosted HTML page from another computer and demonstrate that Nginx immediately serves the changed content.

## Remote Administration

The evidence includes an SSH service configured to listen on port 22 and a remote login session to:

```text
10.10.145.207
```

A remote client can therefore administer the server without physically editing the server's console.

## Modification Workflow

From the second computer, use the permitted remote administration method and edit:

```text
/var/www/html/index.html
```

For example, with SSH:

```bash
ssh mathan@10.10.145.207
```

Then edit:

```bash
sudo nano /var/www/html/index.html
```

Change a visible value such as the heading or a paragraph.

Save the file and exit.

## Verification

Nginx does not need to be restarted for a static HTML file change.

Verify from the second computer:

```bash
curl http://10.10.145.207
```

The changed text should appear in the response.

A browser can also be refreshed at:

```text
http://10.10.145.207
```

## Important Evidence Note

The supplied screenshots document the SSH setup, remote session, HTML content, and command history. They do not capture a clean before/after pair of the same HTML element from a clearly identified second physical computer.

Therefore, for the competition's final proof, capture these two additional terminal states if permitted:
1. Before modification — show the original HTML response.
2. After modification — show the changed HTML response from the second computer.

This makes the Task 3 evidence unambiguous.

## Result
The architecture supports remote modification because the page is a normal static file served by Nginx. A file change is reflected on the next HTTP request without restarting Nginx.

## Evidence
Five screenshots are included in `evidence/task-3-remote-modification/`.
