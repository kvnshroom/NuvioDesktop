# kvn build of Nuvio Desktop

This branch holds only the automation for a personal Nuvio Desktop build.

- Branch `kvn`: the latest upstream release of
  [NuvioMedia/NuvioDesktop](https://github.com/NuvioMedia/NuvioDesktop) plus a few commits
  on top (the "Are you still watching?" prompt from #862 and the updater pointing at this fork).
- Workflow `kvn desktop build` (daily and on demand): rebases the `kvn` commits onto the
  newest upstream release, builds a Linux x86_64 RPM and AppImage and a macOS arm64 DMG (unsigned),
  and publishes them as a release `<upstream tag>.kvn.<n>`. The app's built-in updater
  picks these releases up.
- If the kvn commits stop applying on a new upstream release, the workflow fails and
  GitHub sends a notification; the installed app keeps working.
- Once upstream ships a kvn feature itself (the "Are you still watching?" PR), the rebase
  leaves our commit out and keeps upstream's version. `UPSTREAMED_FEATURES` in
  `scripts/kvn-prepare.sh` lists each feature with code that proves it is upstream.
- dnf repo on GitHub Pages (metadata only; packages stay in the release, signed with the
  repo GPG key):
  ```
  sudo curl -fsSLo /etc/yum.repos.d/nuvio-kvn.repo https://kvnshroom.github.io/NuvioDesktop/nuvio-kvn.repo
  sudo rpm --import https://kvnshroom.github.io/NuvioDesktop/RPM-GPG-KEY-nuvio-kvn
  ```
- Secrets: `KVN_LOCAL_PROPERTIES_BASE64` (base64 of `local.properties`),
  `KVN_REPO_GPG_PRIVATE_KEY_BASE64` and `KVN_REPO_GPG_PASSPHRASE` (repo signing key).

Stop using it: disable the workflow, reinstall the official app.
