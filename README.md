# Project 9: Network Incident Investigation

A beginner-friendly, controlled investigation of one failed SSH login. The project demonstrates how to correlate a packet capture with Linux authentication logs, build an evidence-based timeline, and state the limits of the available evidence.

## Scenario

From an authorized Windows computer on my lab network, I made one SSH login attempt to my Linux Mint VM using a deliberately nonexistent username. I captured the SSH traffic with `tcpdump` and compared it with the VM's SSH service records from `journalctl`.

This was a controlled lab exercise, not a real attack.

## Environment and tools

- Linux Mint 22.3 VM
- Windows OpenSSH client
- `tcpdump` for a short packet capture
- `journalctl` for SSH service records
- SHA-256 checksums to verify the saved capture and log excerpt after collection

No additional software was installed.

## Investigation workflow

1. Captured one SSH connection on the VM's network interface.
2. Reviewed packet timestamps, TCP endpoints, the SSH client banner, and connection close.
3. Queried SSH service records for the same time window.
4. Correlated the client address and ephemeral port in the capture with the authentication records.
5. Saved an incident timeline and assessed what the evidence supports.
6. Verified the saved PCAP and log excerpt against their SHA-256 checksums.

## Result

The capture and SSH logs matched one connection from the authorized lab client to the VM's SSH service. The server logged a nonexistent username and a failed password attempt. The client reset the connection before an authenticated session was established.

The evidence supports a failed login attempt. It does not show a successful login or establish that the VM was compromised. SSH traffic is encrypted after negotiation, so the packet capture cannot reveal the password or later session contents.

The public incident report uses documentation-only example addresses (`192.0.2.10` and `192.0.2.20`) in place of the lab's private IP addresses. Raw PCAP and unredacted system logs are intentionally excluded because they contain local network and device details.

## Repository contents

- `incident-report.md`: sanitized case timeline, findings, and limitations
- `GIT_SETUP.md`: steps for publishing this project
- `LINKEDIN_POST.md`: an optional post draft
- `.gitignore`: excludes raw evidence and local artifacts

## Scope and limitations

- One controlled attempt from a known lab computer; no unknown or external source was involved.
- The client IP identifies the address observed by the VM, not a person.
- The capture covers only a short time window and a single SSH connection.
- Encrypted SSH payloads are not readable in the capture.
- The checksum check confirms that the saved files matched the recorded checksums at verification time. It does not independently prove who created the evidence or provide a formal chain of custody.

## Safety

This exercise was limited to systems on my own lab network and used one deliberately invalid username. Do not attempt access to systems without authorization.

