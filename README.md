# cuttlefish-autocompiler

## Automated builds

This repository uses GitHub Actions and CircleCI workflows to build the latest
`android-cuttlefish` packages. The `amd64` packages build directly on GitHub's standard runners.
The `arm64` packages build on `amd64` runners using QEMU emulation to avoid the need for arm64
runner capacity. Each build publishes a release with one zip per architecture. Each zip contains
the `.deb` packages produced by `tools/buildutils/build_packages.sh`.

To run the workflows manually, use **Actions → Build Cuttlefish Packages → Run workflow** for
amd64 and **Actions → Build Cuttlefish Packages (arm64 emulated) → Run workflow** for arm64.

## CircleCI

CircleCI mirrors the GitHub Actions build by using machine executors for both architectures and
creating a GitHub Release with timestamped tags. Configure the `GH_TOKEN` environment variable in
CircleCI with a GitHub token that has permission to create releases. The CircleCI workflow runs on
each commit to `main` and on the scheduled `0 3 * * *` (Daily at 03:00 UTC) cron for the `main`
branch.
