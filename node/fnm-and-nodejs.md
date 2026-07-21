# fnm and Node.js — what they are and why we need them

> Category: node
> Date: 2026-07-21

## What Node.js is

Node.js is a runtime environment that lets you run JavaScript outside the browser.

Without Node.js, JavaScript can only run inside a browser (Chrome, Safari, etc).
Node.js lets you run JavaScript on your machine or a server — the same way Python
runs Python scripts outside a browser.

Analogy: Node.js is to JavaScript what the Python interpreter is to Python.

## What npm is

npm (Node Package Manager) comes bundled with Node.js.
It installs and manages JavaScript libraries (packages), the same way pip does for Python.

## What fnm is

fnm (Fast Node Manager) is a Node.js version manager.
It lets you install multiple versions of Node.js and switch between them per project.

Analogy: fnm is to Node.js what pyenv is to Python.

## Why we need fnm instead of just installing Node.js directly

Different projects often require different Node.js versions.
fnm lets you pin a version per project using a .node-version file.
When you cd into that folder, fnm automatically switches to the right version.

Without fnm, you would have one global Node.js version and no easy way to switch.

## Why we installed Node.js v22 (not v24)

Node.js follows a release cycle:
- Even-numbered versions (v20, v22, v24...) become LTS (Long Term Support)
- Odd-numbered versions are short-lived

As of July 2026:
- v22 (Jod) = Active LTS — stable, recommended for production and learning
- v24 (Krypton) = Current — not yet LTS, may have breaking changes

We chose v22.23.1 for stability.

## Why we need Node.js for this project

Next.js (the framework we use to build the translation site) runs on Node.js.
npm is used to install Next.js and all its dependencies.

```
Stack relationship:
  our code (Next.js)
       ↓ runs on
    Node.js
       ↓ managed by
       fnm
```