# Source and release notes

This repository is a public recovery snapshot for NABU and UnityStack of the MIT-licensed
`acsystems/keycloak-php-sdk` package. The Composer package name and `Keycloak`
namespace are retained for compatibility with existing applications.

## Verified source

- Upstream version: `4.4.0`.
- Original repository: <https://bitbucket.org/acwebdev/keycloak-php-sdk>.
- Recovery mirror: <https://gitlab.uzh.ch/ini-itkoord-public/keycloak-php-sdk>.
- Original commit: `29545022aea3f317bdbb0539f160914c6afb2183`.
- Original Git tree: `45176c24c048f38c966c8a950fbc05bb970ebafc`.
- Recovered and checked on 22 October 2026, Australia/Brisbane.

The original commit was retrieved from the recovery mirror. Its 48-file tree
matches the installed production copies. Excluding `tests/.env`, its other 47
files were verified against the matching installed UnityStack SDK and the reviewed recovery copy,
using the following SHA-256 manifest before making the fork's packaging edits:

`93f508ac35f57e8fb7d6ea16b8c9cf31a34bb433237e6987ab44bfd851f6abee`

The manifest sorts relative paths and hashes the concatenation of each path,
a NUL byte, its lowercase SHA-256 file digest, and a newline. This fork adds a
README introduction and an ignore rule for `tests/.env`. It omits that test
credentials file and the stale upstream development `composer.lock`; a library's
development lock is not used by consuming applications. The PHP source,
dependency constraints, and original MIT license are unchanged. The original
Git history is not included in the published branch.

## Release v4.4.1

This release restores a controlled source for NABU and UnityStack after the upstream download
became unavailable. It contains no SDK behavior changes or new security fixes.
Upstream is marked abandoned on Packagist; this snapshot does not establish
compatibility with additional Keycloak versions.

## Composer usage

Add this repository to each consuming application's root `composer.json`, ahead
of other repositories:

```json
{
    "type": "vcs",
    "url": "https://github.com/tiran133/keycloak-php-sdk.git",
    "only": ["acsystems/keycloak-php-sdk"]
}
```

Then run a scoped update and commit both Composer files:

```sh
composer update acsystems/keycloak-php-sdk --no-scripts --no-plugins
```

Existing constraints `^4.2` and `^4.4` accept `4.4.1`. A dependency's own
repository declarations are not inherited, so the root application must declare
this source even when the SDK is required indirectly by a core package.

This repository and its release archives are public. Development, CI, and
deployment can download the SDK without GitHub credentials. GitHub authentication
is optional for higher API rate limits; keep any tokens or SSH private keys
outside `composer.json` and Git. Other private application dependencies still
require their own access configuration.

The upstream integration tests create and delete a Keycloak realm. Run them only
against a disposable test realm, with credentials supplied locally; they are not
part of the publication verification.
