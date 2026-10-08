# Task 2 — Access the Hosted Page from Another Computer

## Objective
Make the Nginx-hosted page reachable from another computer connected to the same network.

## Network Information
The server interface was checked with:

```bash
ip -br a
```

The server address shown in the evidence is:
```text
10.10.145.207/20
```

The routing table also shows:
```text
10.10.144.1
```
as the gateway.

## Remote Access Preparation

SSH was enabled to support remote administration:

```bash
sudo systemctl start ssh
sudo systemctl status ssh
```

The SSH service reported:
```text
Server listening on 0.0.0.0 port 22.
Server listening on :: port 22.
```

A remote SSH connection to the server address was also captured in the evidence.

## HTTP Verification

The custom page was queried using:

```bash
curl http://10.10.145.207
```

The returned HTML includes the organizer page content, demonstrating that the server is serving the intended file.

## Important Scoring Requirement

The competition specifically requires access from **another computer on the same network**.

The screenshots provide network, HTTP, and remote-session evidence, but the final organizer demonstration should explicitly use a second physical computer. On that second computer run:

```bash
curl http://10.10.145.207
```

or open:

```text
http://10.10.145.207
```

in a browser.

## Result
The server is configured on the LAN address `10.10.145.207`, Nginx is reachable, and the custom HTML response is available.

## Evidence
Five screenshots are included in `evidence/task-2-remote-access/`.

## Organizer Demonstration
Use a second laptop/PC on the same network and show the address in a browser or terminal.
