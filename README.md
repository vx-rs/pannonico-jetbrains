# Pannonico for JetBrains IDEs

This plugin targets IntelliJ Platform 2026.2, build branch 262, only:

```text
sinceBuild = 262
untilBuild = 262.*
```

It uses the current `LspIntegrationProvider` API and starts the exact pinned
`pannonico-lsp.wasm` through verified Wasmtime 48.0.1 for each marked project
root containing `.pannonico` or `pannonico.yaml`. HTML and Markdown are
supported without redefining their IDE language implementations. The plugin ZIP
contains neither the LSP nor Wasmtime.

The plugin uses platform modules shared by the JetBrains 262 family and does
not depend on `com.intellij.modules.ultimate`. Unified IntelliJ IDEA is the
single automated representative: its free tier includes core HTML support and
continues after the optional Ultimate trial expires. Publish only after the
current IntelliJ IDEA release passes Plugin Verifier and the installed
Starter/Driver scenario. Other JetBrains products are not tested as separate
copies of that same platform-level integration; their own licensing still
applies.

A new IntelliJ IDEA installation may show an optional Ultimate trial tab or
badge. Neither activation nor a paid subscription is required for Pannonico's
HTML acceptance scenario.

After Marketplace publication, install the plugin in IntelliJ IDEA 2026.2:

1. Open **Settings** or **Preferences**, then **Plugins**.
2. Open **Marketplace**, search for `Pannonico`, and select **Install**.
3. Restart the IDE when requested.
4. Open a project whose root contains `pannonico.yaml` or `.pannonico`.
5. Open an HTML or Markdown file below that root.

To install the exact GitHub Release before Marketplace approval, download
`pannonico-jetbrains.zip` from the matching signed release. In **Plugins**, use
the gear menu and **Install Plugin from Disk**, select the ZIP without
extracting or repackaging it, and restart the IDE. This is a user installation
path; release acceptance remains the automated Starter/Driver test.

For offline use, configure both exact pinned files in the IDE VM options:

```text
-Dpannonico.lsp.wasm.path=/absolute/path/to/pannonico-lsp.wasm
-Dpannonico.wasmtime.path=/absolute/path/to/wasmtime
```

Wasmtime is not bundled or republished. Pannonico selects official Wasmtime
48.0.1 under `Apache-2.0 WITH LLVM-exception`; see
<https://github.com/bytecodealliance/wasmtime/releases/tag/v48.0.1>.

The plugin is available without charge. Pannonico product use remains subject
to the licenses included with the release.

Read [SUPPORT.md](SUPPORT.md) before filing a
[JetBrains plugin issue](https://github.com/vx-rs/pannonico-jetbrains/issues).
Report suspected vulnerabilities through the private process in
[SECURITY.md](SECURITY.md), not through a public issue.
