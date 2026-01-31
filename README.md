# cuttlefish-autocompiler

## Automated builds

This repository uses a GitHub Actions workflow to build the latest `android-cuttlefish`
packages for `amd64` and `arm64`, then publishes a release with one zip per architecture.
Each zip contains the `.deb` packages produced by `tools/buildutils/build_packages.sh`.

To run the workflow manually, use **Actions → Build Cuttlefish Packages → Run workflow**.
