# GitHub setup

Suggested repository name: `project9-network-incident-investigation`

## 1. Create the repository

On GitHub, create a new **public** repository named `project9-network-incident-investigation`. Leave it empty (do not initialize it with a README, license, or `.gitignore`).

## 2. Put the public files in a project folder

Copy these files from this package into one new local folder:

- `README.md`
- `incident-report.md`
- `.gitignore`
- `GIT_SETUP.md`
- `LINKEDIN_POST.md`

Do not copy the raw `ssh-attempt.pcap`, `auth-log.txt`, or `checksums.sha256` from the VM into the public repository. The `.gitignore` also excludes them if they are copied by mistake.

## 3. Initialize and publish

Open a terminal in the folder containing those five public files, then run:

```bash
git init -b main
git add README.md incident-report.md .gitignore GIT_SETUP.md LINKEDIN_POST.md
git status --short
git commit -m "Add network incident investigation case study"
git remote add origin https://github.com/Notme3za/project9-network-incident-investigation.git
git push -u origin main
```

Before committing, check `git status --short` and confirm no raw PCAP, unredacted log, or local checksum file is listed. If Git reports that a remote named `origin` already exists, stop and inspect it with `git remote -v` before changing anything.

