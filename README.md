[update-readmes]   Mode: rewrite — migrating to template structure...
# setup-node

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/setup-node)

<!-- AI:start:what-it-does -->
_Description pending._
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
_Architecture documentation pending._
<!-- AI:end:architecture -->

## Install

<!-- Add installation instructions here. This section is yours — the AI will not modify it. -->

```bash
git clone https://github.com/Interested-Deving-1896/setup-node.git
cd setup-node
```

## Usage


See [action.yml](action.yml)

<!-- start usage -->
```yaml
- uses: actions/setup-node@v6
  with:
    # Version Spec of the version to use in SemVer notation.
    # It also admits such aliases as lts/*, latest, nightly and canary builds
    # Examples: 12.x, 10.15.1, >=10.15.0, lts/Hydrogen, 16-nightly, latest, node
    node-version: ''

    # File containing the version Spec of the version to use.  Examples: package.json, .nvmrc, .node-version, .tool-versions.
    # If node-version and node-version-file are both provided the action will use version from node-version.
    node-version-file: ''

    # Set this option if you want the action to check for the latest available version
    # that satisfies the version spec.
    # It will only get affect for lts Nodejs versions (12.x, >=10.15.0, lts/Hydrogen).
    # Default: false
    check-latest: false

    # Target architecture for Node to use. Examples: x86, x64. Will use system architecture by default.
    # Default: ''. The action use system architecture by default
    architecture: ''

    # Used to pull node distributions from https://github.com/actions/node-versions.
    # Since there's a default, this is typically not supplied by the user.
    # When running this action on github.com, the default value is sufficient.
    # When running on GHES, you can pass a personal access token for github.com if you are experiencing rate limiting.
    #
    # We recommend using a service account with the least permissions necessary. Also
    # when generating a new PAT, select the least scopes necessary.
    #
    # [Learn more about creating and using encrypted secrets](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets)
    #
    # Default: ${{ github.server_url == 'https://github.com' && github.token || '' }}
    token: ''

    # Used to specify a package manager for caching in the default directory. Supported values: npm, yarn, pnpm.
    # Package manager should be pre-installed
    # Default: ''
    cache: ''

    # Controls automatic caching for npm. By default, caching for npm is enabled if either the devEngines.packageManager field or the top-level packageManager field in package.json specifies npm and no explicit cache input is provided.
    # To disable automatic caching for npm, set package-manager-cache to false.
    # default: true
    package-manager-cache: true

    # Used to specify the path to a dependency file: package-lock.json, yarn.lock, etc.
    # It will generate hash from the target file for primary key. It works only If cache is specified.
    # Supports wildcards or a list of file names for caching multiple dependencies.
    # Default: ''
    cache-dependency-path: ''

    # Optional registry to set up for auth. Will set the registry in a project level .npmrc and .yarnrc file,
    # and set up auth to read in from env.NODE_AUTH_TOKEN.
    # Default: ''
    registry-url: ''

    # Optional scope for authenticating against scoped registries.
    # Will fall back to the repository owner when using the GitHub Packages registry (https://npm.pkg.github.com/).
    # Default: ''
    scope: ''

    # Optional mirror to download binaries from.
    # Artifacts need to match the official Node.js
    # Example:
    # V8 Canary Build: <mirror_url>/download/v8-canary
    # RC Build: <mirror_url>/download/rc
    # Official: Build <mirror_url>/dist
    # Nightly build: <mirror_url>/download/nightly
    # Default: ''
    mirror: ''

    # Optional mirror token.
    # The token will be used as a bearer token in the Authorization header
    # Default: ''
    mirror-token: ''
```
<!-- end usage -->

**Basic:**

```yaml
steps:
- uses: actions/checkout@v6
- uses: actions/setup-node@v6
  with:
    node-version: 24
- run: npm ci
- run: npm test
```

The `node-version` input is optional. If not supplied, the node version from PATH will be used. However, it is recommended to always specify Node.js version and not rely on the system one.

The action will first check the local cache for a semver match. If unable to find a specific version in the cache, the action will attempt to download a version of Node.js. It will pull LTS versions from [node-versions releases](https://github.com/actions/node-versions/releases) and on miss or failure will fall back to the previous behavior of downloading directly from [node dist](https://nodejs.org/dist/).

For information regarding locally cached versions of Node.js on GitHub hosted runners, check out [GitHub Actions Runner Images](https://github.com/actions/runner-images).

### Supported version syntax

The `node-version` input supports the Semantic Versioning Specification, for more detailed examples please refer to [the semver package documentation](https://github.com/npm/node-semver).

Examples:

 - Major versions: `22`, `24`
 - More specific versions: `20.19`, `22.17.1` , `24.8.0`
 - NVM LTS syntax: `lts/iron`, `lts/jod`, `lts/*`, `lts/-n`
 - Latest release: `*` or `latest`/`current`/`node`

**Note:** Like the other values, `*` will get the latest [locally-cached Node.js version](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2204-Readme.md#nodejs), or the latest version from [actions/node-versions](https://github.com/actions/node-versions/blob/main/versions-manifest.json), depending on the [`check-latest`](docs/advanced-usage.md#check-latest-version) input.

`current`/`latest`/`node` always resolve to the latest [dist version](https://nodejs.org/dist/index.json).
That version is then downloaded from actions/node-versions if possible, or directly from Node.js if not.
Since it will not be cached always, there is possibility of hitting rate limit when downloading from dist

### Checking in lockfiles

It's **strongly recommended** to commit the lockfile of your package manager for security and performance reasons. For more information consult the "Working with lockfiles" section of the [Advanced usage](docs/advanced-usage.md#working-with-lockfiles) guide.

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
_CI documentation pending._
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/setup-node`](https://github.com/Interested-Deving-1896/setup-node) and mirrored through:

```
Interested-Deving-1896/setup-node  ──►  OpenOS-Project-OSP/setup-node  ──►  OpenOS-Project-Ecosystem-OOC/setup-node
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
_Contributors pending._
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream fork._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## License

<!-- AI:start:license -->
[MIT](https://github.com/Interested-Deving-1896/setup-node/blob/main/LICENSE) © 2026 [Interested-Deving-1896](https://github.com/Interested-Deving-1896)
<!-- AI:end:license -->
