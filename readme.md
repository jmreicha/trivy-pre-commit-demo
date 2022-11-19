# Trivy as pre-commit hook show case

## Setup


```sh
pre-commit install
```

## Demo

Append some demo aws credentials to the Dockerfile

```sh
./make_unsecure_changes.sh
```

```sh
git commit -am "added some envs"
```

pre-commit will complain about the aws credentials (three times as the hooks are doing the same)

```
trivyfs-docker...........................................................Failed
- hook id: trivyfs-docker
- exit code: 1

2022-11-19T19:14:07.680Z	[34mINFO[0m	Need to update DB
2022-11-19T19:14:07.680Z	[34mINFO[0m	DB Repository: ghcr.io/aquasecurity/trivy-db
2022-11-19T19:14:07.680Z	[34mINFO[0m	Downloading DB...
2.05 MiB / 35.21 MiB [--->___________________________________________________________] 5.82% ? p/s ?4.86 MiB / 35.21 MiB [-------->_____________________________________________________] 13.81% ? p/s ?7.37 MiB / 35.21 MiB [------------>_________________________________________________] 20.93% ? p/s ?9.95 MiB / 35.21 MiB [------------->___________________________________] 28.26% 13.14 MiB p/s ETA 1s12.66 MiB / 35.21 MiB [----------------->______________________________] 35.97% 13.14 MiB p/s ETA 1s15.35 MiB / 35.21 MiB [-------------------->___________________________] 43.59% 13.14 MiB p/s ETA 1s17.90 MiB / 35.21 MiB [------------------------>_______________________] 50.85% 13.15 MiB p/s ETA 1s20.47 MiB / 35.21 MiB [--------------------------->____________________] 58.14% 13.15 MiB p/s ETA 1s23.35 MiB / 35.21 MiB [------------------------------->________________] 66.32% 13.15 MiB p/s ETA 0s25.74 MiB / 35.21 MiB [----------------------------------->____________] 73.09% 13.14 MiB p/s ETA 0s28.46 MiB / 35.21 MiB [-------------------------------------->_________] 80.82% 13.14 MiB p/s ETA 0s30.98 MiB / 35.21 MiB [------------------------------------------>_____] 87.98% 13.14 MiB p/s ETA 0s33.84 MiB / 35.21 MiB [---------------------------------------------->_] 96.10% 13.17 MiB p/s ETA 0s35.21 MiB / 35.21 MiB [---------------------------------------------->] 100.00% 13.17 MiB p/s ETA 0s35.21 MiB / 35.21 MiB [---------------------------------------------->] 100.00% 13.17 MiB p/s ETA 0s35.21 MiB / 35.21 MiB [---------------------------------------------->] 100.00% 12.46 MiB p/s ETA 0s35.21 MiB / 35.21 MiB [---------------------------------------------->] 100.00% 12.46 MiB p/s ETA 0s35.21 MiB / 35.21 MiB [---------------------------------------------->] 100.00% 12.46 MiB p/s ETA 0s35.21 MiB / 35.21 MiB [-------------------------------------------------] 100.00% 10.30 MiB p/s 3.6s2022-11-19T19:14:12.120Z	[34mINFO[0m	Vulnerability scanning is enabled
2022-11-19T19:14:12.120Z	[34mINFO[0m	Secret scanning is enabled
2022-11-19T19:14:12.120Z	[34mINFO[0m	If your scanning is slow, please try '--security-checks vuln' to disable secret scanning
2022-11-19T19:14:12.120Z	[34mINFO[0m	Please see also https://aquasecurity.github.io/trivy/v0.34/docs/secret/scanning/#recommendation for faster secret detection
2022-11-19T19:14:12.144Z	[34mINFO[0m	Number of language-specific files: 0

Dockerfile (secrets)
====================
Total: 2 (UNKNOWN: 0, LOW: 0, MEDIUM: 0, HIGH: 0, CRITICAL: 2)

CRITICAL: AWS (aws-access-key-id)
════════════════════════════════════════
AWS Access Key ID
────────────────────────────────────────
 Dockerfile:2
────────────────────────────────────────
   1   FROM ubuntu:22.04
   2 [ ENV AWS_ACCESS_KEY_ID=********************
   3   ENV AWS_SECRET_ACCESS_KEY=****************************************
────────────────────────────────────────


CRITICAL: AWS (aws-secret-access-key)
════════════════════════════════════════
AWS Secret Access Key
────────────────────────────────────────
 Dockerfile:3
────────────────────────────────────────
   1   FROM ubuntu:22.04
   2   ENV AWS_ACCESS_KEY_ID=********************
   3 [ ENV AWS_SECRET_ACCESS_KEY=****************************************
   4   
────────────────────────────────────────



```