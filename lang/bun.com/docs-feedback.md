---
url: https://bun.com/docs/feedback
title: Feedback - Bun
source_domain: bun.com
---

# Feedback - Bun

Whether you’ve found a bug, have a performance issue, or just want to suggest an improvement, here’s how you can open a helpful issue:

For general questions, please join our [Discord](https://bun.com/discord).

## [​](https://bun.com/docs/feedback#reporting-issues) Reporting Issues

1

Upgrade Bun

Try upgrading Bun to the latest version with `bun upgrade`. This might fix your problem without having to open an issue.

terminal

Copy

```
bun upgrade
```

You can also try the latest canary release, which includes the most recent changes and bug fixes that haven’t been released in a stable version yet.

terminal

Copy

```
bun upgrade --canary

# To revert back to the stable
bun upgrade --stable
```

If the issue still persists after upgrading, continue to the next step.

2

Review Existing Issues

First take a minute to check if the issue has already been reported. Don’t open a new issue if it has already been reported, it saves time for everyone and helps us focus on fixing things faster.

* 🔍 [**Search existing issues**](https://github.com/oven-sh/bun/issues)
* 💬 [**Check discussions**](https://github.com/oven-sh/bun/discussions)

If you find a related issue, add a 👍 reaction or comment with extra details instead of opening a new one.

3

Report the Issue

If no one has reported the issue, please open a new issue or suggest an improvement.

* 🐞 [**Report a Bug**](https://github.com/oven-sh/bun/issues/new?template=2-bug-report.yml)
* ⚡ [**Suggest an Improvement**](https://github.com/oven-sh/bun/issues/new?template=4-feature-request.yml)

Please provide as much detail as possible, including:

* A clear and concise title
* A code example or steps to reproduce the issue
* The version of Bun you are using (run `bun --version`)
* A detailed description of the issue (what happened, what you expected to happen, and what actually happened)
* The operating system and version you are using

  + For MacOS and Linux: copy the output of `uname -mprs`
  + For Windows: copy the output of this command in the powershell console:
    `"$([Environment]::OSVersion | ForEach-Object VersionString) $(if ([Environment]::Is64BitOperatingSystem) { "x64" } else { "x86" })"`

The Bun team will review the issue and get back to you as soon as possible!

---

## [​](https://bun.com/docs/feedback#use-bun-feedback) Use `bun feedback`

Alternatively, you can use `bun feedback` to share feedback, bug reports, and feature requests directly with the Bun team.

terminal

Copy

```
bun feedback "Love the new release!"
bun feedback report.txt details.log
echo "please document X" | bun feedback --email [email protected]
```

You can provide feedback as text arguments, file paths, or piped input.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/feedback.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /feedback)

⌘I