# Security policy

BranchKit confines every plugin to what its manifest declares and the user
allowed: files, network hosts, privileges. A flaw in that confinement matters
more than most bugs, so please report it privately.

## Reporting a vulnerability

Use **Report a vulnerability** on the Security tab of the repository the
problem is in (for example
[plugin-sdk-go](https://github.com/branchkit/plugin-sdk-go/security/advisories/new)).
If you're not sure which repository, any of them reaches us. Please don't
open a public issue.

Worth reporting privately:

- a way for a plugin to get outside its sandbox (files, network, processes);
- a plugin acting without a privilege or grant the platform should require;
- an SDK or the CLI getting a permission or verification check wrong;
- a way to tamper with a plugin between the registry and a user's machine.

The BranchKit application is pre-launch and not public. Reports about how it
behaves are welcome through any repository here.

## What to expect

We read every report and reply in the private advisory, where we'll work out a
fix and a disclosure date with you. There is no bug bounty.

## Supported versions

The latest release of each SDK and of the CLI. The projects are 0.x, so fixes
land in a new release rather than being backported.
