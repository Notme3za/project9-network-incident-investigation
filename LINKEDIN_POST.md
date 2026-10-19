# LinkedIn post draft

I’ve completed Project 9 in my cybersecurity portfolio: a small, controlled network incident investigation.

I generated one failed SSH login from my own lab computer, captured the connection with `tcpdump`, and correlated the packet timestamps and connection details with Linux SSH authentication records. I then built a timeline, recorded the findings and limitations, and verified the saved evidence files with SHA-256 checksums.

The main lesson was to distinguish what the evidence supports from what it does not: this case showed a failed login attempt, not a successful compromise. The packet capture also showed the limits of network evidence when SSH session contents are encrypted.

The public case report is sanitized and does not include the raw capture or unredacted logs.

#Cybersecurity #Linux #IncidentResponse #NetworkSecurity #LearningByDoing

