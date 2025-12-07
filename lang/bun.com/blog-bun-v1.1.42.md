---
url: https://bun.com/blog/bun-v1.1.42
title: Bun v1.1.42 | Bun Blog
source_domain: bun.com
---

# Bun v1.1.42 | Bun Blog

# Bun v1.1.42

---

[Jarred Sumner](https://twitter.com/jarredsumner) · December 21, 2024

We're hiring [systems engineers](https://bun.com/careers) in San Francisco to build the future of JavaScript!

This release fixes 1 regression from Bun v1.1.41 involving `"use strict"` in empty files and impacting Prisma.

#### To install Bun

curl

npm

powershell

scoop

brew

docker

curl

```
curl -fsSL https://bun.sh/install | bash
```

npm

```
npm install -g bun
```

powershell

```
powershell -c "irm bun.sh/install.ps1|iex"
```

scoop

```
scoop install bun
```

brew

```
brew tap oven-sh/bun
```

```
brew install bun
```

docker

```
docker pull oven/bun
```

```
docker run --rm --init --ulimit memlock=-1:-1 oven/bun
```

#### To upgrade Bun

```
bun upgrade
```

## [Fixed: `"use strict"` regression](https://bun.com/blog/bun-v1.1.42#fixed-use-strict-regression)

Bun v1.1.41 introduced a regression where `"use strict"` in otherwise empty files could cause a crash. We've added regression tests to ensure this doesn't happen again.

---

[#### Bun v1.1.41](https://bun.com/blog/bun-v1.1.41)[#### Bun v1.1.43](https://bun.com/blog/bun-v1.1.43)