# How to verify GitHub's SSH host key fingerprint

> Category: security, git
> Date: 2026-06-19
> Related: SC exam (MITM, PKI, chain of trust, TOFU)

## Why it matters

When connecting to GitHub via SSH for the first time, you need to verify
that the server you're connecting to is the real GitHub, not an attacker
sitting in the middle (man-in-the-middle attack).

If an attacker intercepts the connection, their server's fingerprint will
differ from GitHub's real one. Always verify before typing "yes".

## GitHub's official fingerprints (as of 2026)

| Algorithm | Fingerprint |
|---|---|
| Ed25519 | SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU |
| RSA | SHA256:uNiVztksCsDhcc0u9e8BujQXVUpKZIDTMczCvj3tD2s |
| ECDSA | SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM |

## How to verify

Method 1 — official docs (bookmark this):
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints

Method 2 — command line only (useful when no browser is available):
curl https://api.github.com/meta | grep -A5 "ssh_keys"

## Connection to SC exam

- MITM (man-in-the-middle attack): fingerprint mismatch is how you detect it
- TOFU (Trust On First Use): SSH stores the fingerprint in ~/.ssh/known_hosts on first connect and compares it on every subsequent connection
- Chain of trust: the official docs themselves are served over HTTPS/TLS, so the certificate chain is the root of trust — a practical example of PKI
