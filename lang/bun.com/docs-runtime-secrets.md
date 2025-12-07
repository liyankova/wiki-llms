---
url: https://bun.com/docs/runtime/secrets
title: Secrets - Bun
source_domain: bun.com
---

# Secrets - Bun

Store and retrieve sensitive credentials securely using the operating system’s native credential storage APIs.

This API is new and experimental. It may change in the future.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import { secrets } from "bun";

let githubToken: string | null = await secrets.get({
  service: "my-cli-tool",
  name: "github-token",
});

if (!githubToken) {
  githubToken = prompt("Please enter your GitHub token");

  await secrets.set({
    service: "my-cli-tool",
    name: "github-token",
    value: githubToken,
  });

  console.log("GitHub token stored");
}

const response = await fetch("https://api.github.com/user", {
  headers: { Authorization: `token ${githubToken}` },
});

console.log(`Logged in as ${(await response.json()).login}`);
```

---

## [​](https://bun.com/docs/runtime/secrets#overview) Overview

`Bun.secrets` provides a cross-platform API for managing sensitive credentials that CLI tools and development applications typically store in plaintext files like `~/.npmrc`, `~/.aws/credentials`, or `.env` files. It uses:

* **macOS**: Keychain Services
* **Linux**: libsecret (GNOME Keyring, KWallet, etc.)
* **Windows**: Windows Credential Manager

All operations are asynchronous and non-blocking, running on Bun’s threadpool.

In the future, we may add an additional `provider` option to make this better for production deployment secrets, but
today this API is mostly useful for local development tools.

---

## [​](https://bun.com/docs/runtime/secrets#api) API

### [​](https://bun.com/docs/runtime/secrets#bun-secrets-get-options) `Bun.secrets.get(options)`

Retrieve a stored credential.

Copy

```
import { secrets } from "bun";

const password = await Bun.secrets.get({
  service: "my-app",
  name: "[email protected]",
});
// Returns: string | null

// Or if you prefer without an object
const password = await Bun.secrets.get("my-app", "[email protected]");
```

**Parameters:**

* `options.service` (string, required) - The service or application name
* `options.name` (string, required) - The username or account identifier

**Returns:**

* `Promise<string | null>` - The stored password, or `null` if not found

### [​](https://bun.com/docs/runtime/secrets#bun-secrets-set-options,-value) `Bun.secrets.set(options, value)`

Store or update a credential.

Copy

```
import { secrets } from "bun";

await secrets.set({
  service: "my-app",
  name: "[email protected]",
  value: "super-secret-password",
});
```

**Parameters:**

* `options.service` (string, required) - The service or application name
* `options.name` (string, required) - The username or account identifier
* `value` (string, required) - The password or secret to store

**Notes:**

* If a credential already exists for the given service/name combination, it will be replaced
* The stored value is encrypted by the operating system

### [​](https://bun.com/docs/runtime/secrets#bun-secrets-delete-options) `Bun.secrets.delete(options)`

Delete a stored credential.

Copy

```
const deleted = await Bun.secrets.delete({
  service: "my-app",
  name: "[email protected]",
  value: "super-secret-password",
});
// Returns: boolean
```

**Parameters:**

* `options.service` (string, required) - The service or application name
* `options.name` (string, required) - The username or account identifier

**Returns:**

* `Promise<boolean>` - `true` if a credential was deleted, `false` if not found

---

## [​](https://bun.com/docs/runtime/secrets#examples) Examples

### [​](https://bun.com/docs/runtime/secrets#storing-cli-tool-credentials) Storing CLI Tool Credentials

Copy

```
// Store GitHub CLI token (instead of ~/.config/gh/hosts.yml)
await Bun.secrets.set({
  service: "my-app.com",
  name: "github-token",
  value: "ghp_xxxxxxxxxxxxxxxxxxxx",
});

// Or if you prefer without an object
await Bun.secrets.set("my-app.com", "github-token", "ghp_xxxxxxxxxxxxxxxxxxxx");

// Store npm registry token (instead of ~/.npmrc)
await Bun.secrets.set({
  service: "npm-registry",
  name: "https://registry.npmjs.org",
  value: "npm_xxxxxxxxxxxxxxxxxxxx",
});

// Retrieve for API calls
const token = await Bun.secrets.get({
  service: "gh-cli",
  name: "github.com",
});

if (token) {
  const response = await fetch("https://api.github.com/name", {
    headers: {
      Authorization: `token ${token}`,
    },
  });
}
```

### [​](https://bun.com/docs/runtime/secrets#migrating-from-plaintext-config-files) Migrating from Plaintext Config Files

Copy

```
// Instead of storing in ~/.aws/credentials
await Bun.secrets.set({
  service: "aws-cli",
  name: "AWS_SECRET_ACCESS_KEY",
  value: process.env.AWS_SECRET_ACCESS_KEY,
});

// Instead of .env files with sensitive data
await Bun.secrets.set({
  service: "my-app",
  name: "api-key",
  value: "sk_live_xxxxxxxxxxxxxxxxxxxx",
});

// Load at runtime
const apiKey =
  (await Bun.secrets.get({
    service: "my-app",
    name: "api-key",
  })) || process.env.API_KEY; // Fallback for CI/production
```

### [​](https://bun.com/docs/runtime/secrets#error-handling) Error Handling

Copy

```
try {
  await Bun.secrets.set({
    service: "my-app",
    name: "alice",
    value: "password123",
  });
} catch (error) {
  console.error("Failed to store credential:", error.message);
}

// Check if a credential exists
const password = await Bun.secrets.get({
  service: "my-app",
  name: "alice",
});

if (password === null) {
  console.log("No credential found");
}
```

### [​](https://bun.com/docs/runtime/secrets#updating-credentials) Updating Credentials

Copy

```
// Initial password
await Bun.secrets.set({
  service: "email-server",
  name: "[email protected]",
  value: "old-password",
});

// Update to new password
await Bun.secrets.set({
  service: "email-server",
  name: "[email protected]",
  value: "new-password",
});

// The old password is replaced
```

---

## [​](https://bun.com/docs/runtime/secrets#platform-behavior) Platform Behavior

### [​](https://bun.com/docs/runtime/secrets#macos-keychain) macOS (Keychain)

* Credentials are stored in the name’s login keychain
* The keychain may prompt for access permission on first use
* Credentials persist across system restarts
* Accessible by the name who stored them

### [​](https://bun.com/docs/runtime/secrets#linux-libsecret) Linux (libsecret)

* Requires a secret service daemon (GNOME Keyring, KWallet, etc.)
* Credentials are stored in the default collection
* May prompt for unlock if the keyring is locked
* The secret service must be running

### [​](https://bun.com/docs/runtime/secrets#windows-credential-manager) Windows (Credential Manager)

* Credentials are stored in Windows Credential Manager
* Visible in Control Panel → Credential Manager → Windows Credentials
* Persist with `CRED_PERSIST_ENTERPRISE` flag so it’s scoped per user
* Encrypted using Windows Data Protection API

## [​](https://bun.com/docs/runtime/secrets#security-considerations) Security Considerations

1. **Encryption**: Credentials are encrypted by the operating system’s credential manager
2. **Access Control**: Only the name who stored the credential can retrieve it
3. **No Plain Text**: Passwords are never stored in plain text
4. **Memory Safety**: Bun zeros out password memory after use
5. **Process Isolation**: Credentials are isolated per name account

## [​](https://bun.com/docs/runtime/secrets#limitations) Limitations

* Maximum password length varies by platform (typically 2048-4096 bytes)
* Service and name names should be reasonable lengths (< 256 characters)
* Some special characters may need escaping depending on the platform
* Requires appropriate system services:
  + Linux: Secret service daemon must be running
  + macOS: Keychain Access must be available
  + Windows: Credential Manager service must be enabled

---

## [​](https://bun.com/docs/runtime/secrets#comparison-with-environment-variables) Comparison with Environment Variables

Unlike environment variables, `Bun.secrets`:

* ✅ Encrypts credentials at rest (thanks to the operating system)
* ✅ Avoids exposing secrets in process memory dumps (memory is zeroed after its no longer needed)
* ✅ Survives application restarts
* ✅ Can be updated without restarting the application
* ✅ Provides name-level access control
* ❌ Requires OS credential service
* ❌ Not very useful for deployment secrets (use environment variables in production)

---

## [​](https://bun.com/docs/runtime/secrets#best-practices) Best Practices

1. **Use descriptive service names**: Match the tool or application name
   If you’re building a CLI for external use, you probably should use a UTI (Uniform Type Identifier) for the service name.

   Copy

   ```
   // Good - matches the actual tool
   { service: "com.docker.hub", name: "username" }
   { service: "com.vercel.cli", name: "team-name" }

   // Avoid - too generic
   { service: "api", name: "key" }
   ```
2. **Credentials-only**: Don’t store application configuration in this API
   This API is slow, you probably still need to use a config file for some things.
3. **Use for local development tools**:
   * ✅ CLI tools (gh, npm, docker, kubectl)
   * ✅ Local development servers
   * ✅ Personal API keys for testing
   * ❌ Production servers (use proper secret management)

---

## [​](https://bun.com/docs/runtime/secrets#typescript) TypeScript

Copy

```
namespace Bun {
  interface SecretsOptions {
    service: string;
    name: string;
  }

  interface Secrets {
    get(options: SecretsOptions): Promise<string | null>;
    set(options: SecretsOptions, value: string): Promise<void>;
    delete(options: SecretsOptions): Promise<boolean>;
  }

  const secrets: Secrets;
}
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/secrets.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/secrets)

⌘I