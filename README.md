# Pannonico for JetBrains IDEs

This plugin targets IntelliJ Platform 2026.2, build branch 262, only:

```text
sinceBuild = 262
untilBuild = 262.*
```

It uses the current `LspIntegrationProvider` API and starts one exact native
Pannonico language server for each marked project root containing `.pannonico`
or `pannonico.yaml`. HTML and Markdown are supported without redefining their
IDE language implementations. The plugin ZIP does not contain an LSP binary.

The initial verification matrix is IntelliJ IDEA, WebStorm, PhpStorm, PyCharm,
DataSpell, RubyMine, CLion, DataGrip, GoLand, Rider, and RustRover on the 262
release branch. Claim a product as supported only after its Plugin Verifier and
installed-IDE checks pass. Current IntelliJ IDEA and PyCharm unified products
can expose the LSP functionality without a paid subscription. The plugin
depends on `com.intellij.modules.lsp`, not the subscription-gated
`com.intellij.modules.ultimate`; Android Studio and open-source IntelliJ builds
do not provide this LSP API.

For offline use, configure the exact pinned native binary in the IDE VM options:

```text
-Dpannonico.lsp.path=/absolute/path/to/pannonico-lsp
```

The plugin is available without charge. Pannonico product use remains subject
to the licenses included with the release.

Read [SUPPORT.md](SUPPORT.md) before filing a
[JetBrains plugin issue](https://github.com/vx-rs/pannonico-jetbrains/issues).
Report suspected vulnerabilities through the private process in
[SECURITY.md](SECURITY.md), not through a public issue.
