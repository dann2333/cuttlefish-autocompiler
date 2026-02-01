# cuttlefish-autocompiler

## Automated builds

This repository uses GitHub Actions and CircleCI workflows to build the latest
`android-cuttlefish` packages. Both `amd64` and `arm64` packages are built in parallel
on GitHub's standard amd64 runners. The `arm64` packages use QEMU emulation to avoid
the need for arm64 runner capacity. The unified workflow publishes a single release
containing both architecture packages.

To run the workflow manually, use **Actions → Build Cuttlefish Packages (amd64 + arm64) → Run workflow**.
Legacy architecture-specific workflows are deprecated but available for backward compatibility.

## CircleCI

CircleCI mirrors the GitHub Actions build by using machine executors for both architectures and
creating a GitHub Release with timestamped tags. Configure the `GH_TOKEN` environment variable in
CircleCI with a GitHub token that has permission to create releases. The CircleCI workflow runs on
each commit to `main` and on the scheduled `0 3 * * *` (Daily at 03:00 UTC) cron for the `main`
branch.
