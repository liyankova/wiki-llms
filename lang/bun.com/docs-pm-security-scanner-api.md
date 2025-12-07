---
url: https://bun.com/docs/pm/security-scanner-api
title: Security Scanner API - Bun
source_domain: bun.com
---

# Security Scanner API - Bun

Bun’s package manager can scan packages for security vulnerabilities before installation, helping protect your applications from supply chain attacks and known vulnerabilities.

---

## [​](https://bun.com/docs/pm/security-scanner-api#quick-start) Quick Start

Configure a security scanner in your `bunfig.toml`:

bunfig.toml

Copy

```
[install.security]
scanner = "@acme/bun-security-scanner"
```

When configured, Bun will:

* Scan all packages before installation
* Display security warnings and advisories
* Cancel installation if critical vulnerabilities are found
* Automatically disable auto-install for security

---

## [​](https://bun.com/docs/pm/security-scanner-api#how-it-works) How It Works

Security scanners analyze packages during `bun install`, `bun add`, and other package operations. They can detect:

* Known security vulnerabilities (CVEs)
* Malicious packages
* License compliance issues
* …and more!

### [​](https://bun.com/docs/pm/security-scanner-api#security-levels) Security Levels

Scanners report issues at two severity levels:

* **`fatal`** - Installation stops immediately, exits with non-zero code
* **`warn`** - In interactive terminals, prompts to continue; in CI, exits immediately

---

## [​](https://bun.com/docs/pm/security-scanner-api#using-pre-built-scanners) Using Pre-built Scanners

Many security companies publish Bun security scanners as npm packages that you can install and use immediately.

### [​](https://bun.com/docs/pm/security-scanner-api#installing-a-scanner) Installing a Scanner

Install a security scanner from npm:

terminal

Copy

```
bun add -d @acme/bun-security-scanner
```

Consult your security scanner’s documentation for their specific package name and installation instructions. Most
scanners will be installed with `bun add`.

### [​](https://bun.com/docs/pm/security-scanner-api#configuring-the-scanner) Configuring the Scanner

After installation, configure it in your `bunfig.toml`:

bunfig.toml

Copy

```
[install.security]
scanner = "@acme/bun-security-scanner"
```

### [​](https://bun.com/docs/pm/security-scanner-api#enterprise-configuration) Enterprise Configuration

Some enterprise scanners might support authentication and/or configuration through environment variables:

terminal

Copy

```
# This might go in ~/.bashrc, for example
export SECURITY_API_KEY="your-api-key"

# The scanner will now use these credentials automatically
bun install
```

Consult your security scanner’s documentation to learn which environment variables to set and if any additional configuration is required.

### [​](https://bun.com/docs/pm/security-scanner-api#authoring-your-own-scanner) Authoring your own scanner

For a complete example with tests and CI setup, see the official template:
[github.com/oven-sh/security-scanner-template](https://github.com/oven-sh/security-scanner-template)

## [​](https://bun.com/docs/pm/security-scanner-api#related) Related

* [Configuration (bunfig.toml)](https://bun.com/docs/runtime/bunfig#install-security-scanner)
* [Package Manager](https://bun.com/docs/installation)
* [Security Scanner Template](https://github.com/oven-sh/security-scanner-template)

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/security-scanner-api.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/security-scanner-api)

⌘I