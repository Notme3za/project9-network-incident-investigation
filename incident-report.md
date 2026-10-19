# Project 9 — Network Incident Investigation

## Case summary

This was a controlled lab exercise. From an authorized Windows computer on my lab network, I made one SSH login attempt to my Linux Mint VM using a deliberately nonexistent username.

For privacy, the client and server addresses below are documentation-only examples, not the real lab addresses.

## Evidence reviewed

- `ssh-attempt.pcap`: 22 packets captured; `tcpdump` reported 0 packets dropped.
- `auth-log.txt`: SSH service records from the same time window. The unredacted copy remains in the lab and is not included in this public repository.
- `checksums.sha256`: local SHA-256 checksums for the packet capture and log excerpt; both checks passed after collection. The local checksum file is not included because it contains local file paths.

## Timeline — 2026-10-19 (VM local time, UTC+08:00)

| Time | Evidence | Observation |
|---|---|---|
| 12:02:47 | Packet capture and SSH log | Connection from `192.0.2.10:51359` to `192.0.2.20:22` began. Addresses are anonymized documentation examples. |
| 12:02:47 | Packet capture | The client advertised an OpenSSH for Windows 9.5 banner; SSH negotiation followed. |
| 12:02:47 | SSH log | The server recorded the deliberately nonexistent test username. |
| 12:02:51 | SSH log | The authentication attempt failed for the unknown user. |
| 12:02:53 | SSH log | The server recorded a failed password attempt. |
| 12:02:54 | Packet capture and SSH log | The client reset the connection; the server recorded the close during pre-authentication. |

## Assessment

The packet capture and SSH logs corroborate one SSH login attempt from the authorized lab client. The server rejected the attempt because the username did not exist. This was the deliberate test performed for this case.

The evidence does not show a successful login or establish that the VM was compromised. After SSH negotiation, session contents are encrypted, so the packet capture does not reveal the password or later session contents.

## Limitations

This was a single, controlled attempt from my own lab computer. It does not represent a real attack or demonstrate behavior from an unknown source. The source IP identifies the device address seen by the VM; by itself, it does not identify a person. The logs and capture cover only the recorded time window.

The public version anonymizes the private IP addresses and excludes the raw PCAP, raw SSH logs, and local checksum file. The checksum verification confirms the local files matched their recorded hashes at the time of checking; it is not a formal chain-of-custody process.

