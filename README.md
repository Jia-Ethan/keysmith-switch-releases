# Keysmith Switch Releases

Public updater artifacts for [Keysmith Switch](https://github.com/Jia-Ethan/keysmith-switch).

This repository contains generated release metadata and signed updater artifacts only. Source code and production updater signing keys remain in the private product repository and protected secret storage.

The public workflow accepts a signed source tag and a successful private release run, independently verifies the supported-platform manifest and checksums, and publishes only through the protected `production` environment. Linux validation artifacts never enter the public updater feed.
