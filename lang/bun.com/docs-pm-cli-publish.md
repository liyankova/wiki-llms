---
url: https://bun.com/docs/pm/cli/publish
title: bun publish - Bun
source_domain: bun.com
---

# bun publish - Bun

`bun publish` will automatically pack your package into a tarball, strip catalog and workspace protocols from the `package.json` (resolving versions if necessary), and publish to the registry specified in your configuration files. Both `bunfig.toml` and `.npmrc` files are supported.

terminal

Copy

```
## Publishing the package from the current working directory
bun publish
```

Copy

```
bun publish v1.3.3 (ca7428e9)

packed 203B package.json
packed 224B README.md
packed 30B index.ts
packed 0.64KB tsconfig.json

Total files: 4
Shasum: 79e2b4377b63f4de38dc7ea6e5e9dbee08311a69
Integrity: sha512-6QSNlDdSwyG/+[...]X6wXHriDWr6fA==
Unpacked size: 1.1KB
Packed size: 0.76KB
Tag: latest
Access: default
Registry: http://localhost:4873/

 + [email protected]
```

Alternatively, you can pack and publish your package separately by using `bun pm pack` followed by `bun publish` with the path to the output tarball.

terminal

Copy

```
bun pm pack
...
bun publish ./package.tgz
```

`bun publish` will not run lifecycle scripts (`prepublishOnly/prepack/prepare/postpack/publish/postpublish`) if a
tarball path is provided. Scripts will only be run if the package is packed by `bun publish`.

### [​](https://bun.com/docs/pm/cli/publish#access) `--access`

The `--access` flag can be used to set the access level of the package being published. The access level can be one of `public` or `restricted`. Unscoped packages are always public, and attempting to publish an unscoped package with `--access restricted` will result in an error.

terminal

Copy

```
bun publish --access public
```

`--access` can also be set in the `publishConfig` field of your `package.json`.

package.json

Copy

```
{
  "publishConfig": {
    "access": "restricted"
  }
}
```

### [​](https://bun.com/docs/pm/cli/publish#tag) `--tag`

Set the tag of the package version being published. By default, the tag is `latest`. The initial version of a package is always given the `latest` tag in addition to the specified tag.

terminal

Copy

```
bun publish --tag alpha
```

`--tag` can also be set in the `publishConfig` field of your `package.json`.

package.json

Copy

```
{
  "publishConfig": {
    "tag": "next"
  }
}
```

### [​](https://bun.com/docs/pm/cli/publish#dry-run) `--dry-run`

The `--dry-run` flag can be used to simulate the publish process without actually publishing the package. This is useful for verifying the contents of the published package without actually publishing the package.

terminal

Copy

```
bun publish --dry-run
```

### [​](https://bun.com/docs/pm/cli/publish#tolerate-republish) `--tolerate-republish`

Exit with code 0 instead of 1 if the package version already exists. Useful in CI/CD where jobs may be re-run.

terminal

Copy

```
bun publish --tolerate-republish
```

### [​](https://bun.com/docs/pm/cli/publish#gzip-level) `--gzip-level`

Specify the level of gzip compression to use when packing the package. Only applies to `bun publish` without a tarball path argument. Values range from `0` to `9` (default is `9`).

### [​](https://bun.com/docs/pm/cli/publish#auth-type) `--auth-type`

If you have 2FA enabled for your npm account, `bun publish` will prompt you for a one-time password. This can be done through a browser or the CLI. The `--auth-type` flag can be used to tell the npm registry which method you prefer. The possible values are `web` and `legacy`, with `web` being the default.

terminal

Copy

```
bun publish --auth-type legacy
...
This operation requires a one-time password.
Enter OTP: 123456
...
```

### [​](https://bun.com/docs/pm/cli/publish#otp) `--otp`

Provide a one-time password directly to the CLI. If the password is valid, this will skip the extra prompt for a one-time password before publishing. Example usage:

terminal

Copy

```
bun publish --otp 123456
```

`bun publish` respects the `NPM_CONFIG_TOKEN` environment variable which can be used when publishing in github actions
or automated workflows.

---

## [​](https://bun.com/docs/pm/cli/publish#cli-usage) CLI Usage

terminal

Copy

```
bun publish dist
```

### [​](https://bun.com/docs/pm/cli/publish#publishing-options) Publishing Options

[​](https://bun.com/docs/pm/cli/publish#param-access)

--access

string

The `--access` flag can be used to set the access level of the package being published. The access level can be one of `public` or `restricted`. Unscoped packages are always public, and attempting to publish an unscoped package with `--access restricted` will result in an error.

terminal

Copy

```
bun publish --access public
```

`--access` can also be set in the `publishConfig` field of your `package.json`.

package.json

Copy

```
{
  "publishConfig": {
    "access": "restricted"
  }
}
```

[​](https://bun.com/docs/pm/cli/publish#param-tag)

--tag

string

default:"latest"

Set the tag of the package version being published. By default, the tag is `latest`. The initial version of a package is always given the `latest` tag in addition to the specified tag.

terminal

Copy

```
bun publish --tag alpha
```

`--tag` can also be set in the `publishConfig` field of your `package.json`.

package.json

Copy

```
{
  "publishConfig": {
    "tag": "next"
  }
}
```

[​](https://bun.com/docs/pm/cli/publish#param-dry-run-val)

--dry-run=<val>

string

The `--dry-run` flag can be used to simulate the publish process without actually publishing the package. This is useful for verifying the contents of the published package without actually publishing the package.

Copy

```
bun publish --dry-run
```

[​](https://bun.com/docs/pm/cli/publish#param-gzip-level)

--gzip-level

string

default:"9"

Specify the level of gzip compression to use when packing the package. Only applies to `bun publish` without a tarball
path argument. Values range from `0` to `9` (default is `9`).

[​](https://bun.com/docs/pm/cli/publish#param-auth-type)

--auth-type

string

default:"web"

If you have 2FA enabled for your npm account, `bun publish` will prompt you for a one-time password. This can be done through a browser or the CLI. The `--auth-type` flag can be used to tell the npm registry which method you prefer. The possible values are `web` and `legacy`, with `web` being the default.

terminal

Copy

```
bun publish --auth-type legacy
...
This operation requires a one-time password.
Enter OTP: 123456
...
```

[​](https://bun.com/docs/pm/cli/publish#param-otp)

--otp

string

default:"web"

Provide a one-time password directly to the CLI. If the password is valid, this will skip the extra prompt for a one-time password before publishing. Example usage:

terminal

Copy

```
bun publish --otp 123456
```

`bun publish` respects the `NPM_CONFIG_TOKEN` environment variable which can be used when publishing in github actions
or automated workflows.

### [​](https://bun.com/docs/pm/cli/publish#registry-configuration) Registry Configuration

#### [​](https://bun.com/docs/pm/cli/publish#custom-registry) Custom Registry

[​](https://bun.com/docs/pm/cli/publish#param-registry)

--registry

string

Specify registry URL, overriding .npmrc and bunfig.toml

Copy

```
bun publish --registry https://my-private-registry.com
```

#### [​](https://bun.com/docs/pm/cli/publish#ssl-certificates) SSL Certificates

[​](https://bun.com/docs/pm/cli/publish#param-ca)

--ca

string

Provide Certificate Authority signing certificate

[​](https://bun.com/docs/pm/cli/publish#param-cafile)

--cafile

string

Path to Certificate Authority certificate file

Copy

```
bun publish --ca "-----BEGIN CERTIFICATE-----..."
```

### [​](https://bun.com/docs/pm/cli/publish#publishing-options-2) Publishing Options

#### [​](https://bun.com/docs/pm/cli/publish#dependency-management) Dependency Management

[​](https://bun.com/docs/pm/cli/publish#param-p-production)

-p, --production

boolean

Don’t install devDependencies

[​](https://bun.com/docs/pm/cli/publish#param-omit)

--omit

string

Exclude dependency types: `dev`, `optional`, or `peer`

[​](https://bun.com/docs/pm/cli/publish#param-f-force)

-f, --force

boolean

Always request the latest versions from the registry & reinstall all dependencies

#### [​](https://bun.com/docs/pm/cli/publish#script-control) Script Control

[​](https://bun.com/docs/pm/cli/publish#param-ignore-scripts)

--ignore-scripts

boolean

Skip lifecycle scripts during packing and publishing

[​](https://bun.com/docs/pm/cli/publish#param-trust)

--trust

boolean

Add packages to trustedDependencies and run their scripts

**Lifecycle Scripts** — When providing a pre-built tarball, lifecycle scripts (prepublishOnly, prepack, etc.) are not
executed. Scripts only run when Bun packs the package itself.

#### [​](https://bun.com/docs/pm/cli/publish#file-management) File Management

[​](https://bun.com/docs/pm/cli/publish#param-no-save)

--no-save

boolean

Don’t update package.json or lockfile

[​](https://bun.com/docs/pm/cli/publish#param-frozen-lockfile)

--frozen-lockfile

boolean

Disallow changes to lockfile

[​](https://bun.com/docs/pm/cli/publish#param-yarn)

--yarn

boolean

Generate yarn.lock file (yarn v1 compatible)

#### [​](https://bun.com/docs/pm/cli/publish#performance) Performance

[​](https://bun.com/docs/pm/cli/publish#param-backend)

--backend

string

Platform optimizations: `clonefile` (default), `hardlink`, `symlink`, or `copyfile`

[​](https://bun.com/docs/pm/cli/publish#param-network-concurrency)

--network-concurrency

number

default:"48"

Maximum concurrent network requests

[​](https://bun.com/docs/pm/cli/publish#param-concurrent-scripts)

--concurrent-scripts

number

default:"5"

Maximum concurrent lifecycle scripts

#### [​](https://bun.com/docs/pm/cli/publish#output-control) Output Control

[​](https://bun.com/docs/pm/cli/publish#param-silent)

--silent

boolean

Suppress all output

[​](https://bun.com/docs/pm/cli/publish#param-verbose)

--verbose

boolean

Show detailed logging

[​](https://bun.com/docs/pm/cli/publish#param-no-progress)

--no-progress

boolean

Hide progress bar

[​](https://bun.com/docs/pm/cli/publish#param-no-summary)

--no-summary

boolean

Don’t print publish summary

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/publish.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/publish)

⌘I