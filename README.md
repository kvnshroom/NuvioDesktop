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
- Needs the repository secret `KVN_LOCAL_PROPERTIES_BASE64` (base64 of `local.properties`).

Stop using it: disable the workflow, reinstall the official app.
