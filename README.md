# gl-prebuilds

Self-hosted [prebuild-install](https://github.com/prebuild/prebuild-install)
binaries for [`gl`](https://github.com/stackgl/headless-gl) (headless-gl),
for node ABIs the upstream release doesn't cover. Compiling gl means
compiling ANGLE, which takes tens of minutes per install — these turn that
into a download.

Consumers opt in with an `.npmrc` next to their `package.json`:

```ini
gl_binary_host_mirror=https://github.com/u9g/gl-prebuilds/releases/download
```

prebuild-install then fetches
`…/download/v<version>/gl-v<version>-node-v<abi>-<platform>-<arch>.tar.gz`
and falls back to building from source when the release has no matching
asset.

Assets live on a release tagged `v<gl version>`. The `build` workflow
compiles linux-x64 on a runner and uploads it; darwin-arm64 was built
locally (`node-gyp rebuild` inside `node_modules/gl`, then tar the
`build/Release` runtime artifacts).
