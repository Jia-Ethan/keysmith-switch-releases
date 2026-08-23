# Keysmith Switch Releases

Public updater artifacts for [Keysmith Switch](https://github.com/Jia-Ethan/keysmith-switch).

This repository contains generated release metadata, updater-signed payloads, and the manual bootstrap installer. Source code and production updater signing keys remain in the private product repository and protected secret storage.

The public workflow accepts a signed source tag and a successful private release run, independently verifies the supported-platform manifest, updater signatures, provenance and checksums, and publishes only through the protected `production` environment. Linux validation artifacts never enter the public updater feed.

No updater Release or channel manifest has been published yet. `v0.1.2` is the production updater-key bootstrap: existing `v0.1.1` installs must download it manually, while later releases can use in-app updates from `v0.1.2` onward. Platform code signing is not part of this distribution model; updater payloads remain protected by the production Tauri minisign key.

## Release channels

- Stable metadata: `https://github.com/Jia-Ethan/keysmith-switch-releases/releases/latest/download/latest.json`
- Beta metadata: `https://raw.githubusercontent.com/Jia-Ethan/keysmith-switch-releases/beta/latest.json`
- Immutable version assets: `https://github.com/Jia-Ethan/keysmith-switch-releases/releases/tag/vX.Y.Z`

The repository must contain only the macOS bootstrap DMG, updater-signed payloads, signatures, `latest.json`, `provenance.json`, and `SHA256SUMS.txt`. The private signing key, source archives, standalone Preview artifacts, and unsupported Linux artifacts do not belong here.

## Publication boundary

1. The private source repository builds ad-hoc macOS and unsigned Windows candidates from a GitHub-verified semantic-version tag, then signs updater payloads with the production Tauri key.
2. The public workflow accepts the exact successful source run ID, binds it to the source repository and release workflow path, verifies tag/commit provenance, signatures, platform set, URLs, and SHA-256, then uploads a short-lived verified artifact.
3. The protected `production` environment gates the publishing job. Existing tags and Releases are immutable and are never overwritten.

Required public-repository Secrets are `SOURCE_ARTIFACT_DOWNLOAD_TOKEN`, `SOURCE_REPOSITORY_DEPLOY_KEY_B64`, and `TAURI_UPDATER_PUBLIC_KEY`. The repository deliberately has no production updater private-key Secret.
