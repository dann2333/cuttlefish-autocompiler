# cuttlefish-autocompiler

## Automated builds

This repository uses GitHub Actions to build the latest
[`android-cuttlefish`](https://github.com/google/android-cuttlefish) Debian packages. The
`amd64` and `arm64` packages are built in parallel as a job matrix on GitHub-hosted runners
(`ubuntu-latest` for `amd64`, `ubuntu-24.04-arm` for `arm64`). When both builds succeed, the
unified workflow publishes a single release (tag `cuttlefish-<UTC timestamp>`) containing
`cuttlefish-amd64.zip` and `cuttlefish-arm64.zip`.

The workflow runs daily at `0 3 * * *` (03:00 UTC). To run it manually, use
**Actions → Build Cuttlefish Packages (amd64 + arm64) → Run workflow**.

### Notes

- `bazelisk` is installed explicitly on both architectures with the upstream
  `tools/buildutils/installbazel.sh`. Upstream's `build_packages.sh` skips that step whenever a
  `bazel` binary is already on `PATH`, which is the case on the runner images, yet
  `cuttlefish-common-build-deps` depends on the `bazelisk` apt package.
- Builds need a lot of memory, so a 24 GB swap file is created before every build.

### Legacy workflows

`build-cuttlefish.yml` (amd64) and `build-cuttlefish-arm64.yml` (arm64 emulated with QEMU) are
deprecated, manual-only and kept for backward compatibility. Use the unified workflow instead.
