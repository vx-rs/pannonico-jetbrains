# JetBrains release

## Release history

### 0.6.0

- Select Pannonico LSP 0.6.0 and synchronize YAML and JSON project inputs.
- Add completion and Quick Documentation for project references and compiler
  diagnostics that remain available when a project cannot finish loading.
- Ignore Pannonico-like source inside Markdown code and
  `pannonico-verbatim` wrappers while retaining language features in live
  source.
- Preserve server-filtered completion results in IntelliJ Platform 2026.2.

### 0.5.1

- Add the Marketplace plugin icon.
- List completion, hover, definition, diagnostic, HTML, and Markdown support
  in the plugin description.

### 0.5.0

- Publish the initial JetBrains plugin release for IntelliJ Platform 2026.2.

The initial release is `0.5.0`. Later JetBrains-only changes increment the
JetBrains patch version without forcing unrelated tracks to use the same patch
number.

Pannonico supports only the current JetBrains platform generation. The initial
release uses `sinceBuild = 262` and `untilBuild = 262.*`.

When moving to a new generation, update the build range, IntelliJ Platform
dependency, LSP API, IntelliJ IDEA Plugin Verifier target, installed test, and
documentation together. Do not retain older-generation API compatibility
unless explicitly requested.

## Release artifact

Every LSP release requires a new author-signed plugin ZIP. The GitHub Release
owns the exact reviewed ZIP, and that same file is uploaded unchanged to
JetBrains Marketplace.

Each release machine may use its own unrelated self-signed author certificate.
The certificate may change for a later plugin version; one plugin version must
not be rebuilt or re-signed with a different key.

Upload the GitHub Release ZIP manually to JetBrains Marketplace:

1. Sign in and open **Upload plugin** or **Upload update**.
2. Select the `vx.rs` Vendor profile.
3. Upload the exact `pannonico-jetbrains.zip` from the printed GitHub Release
   URL.
4. Keep the plugin free and use the default release channel.
5. Use [EULA.md](EULA.md) when Marketplace requests the plugin EULA.
6. Submit the plugin for asynchronous review.

Marketplace review is asynchronous, so there is no immediate Marketplace
readback gate. Before publication, the exact signed candidate must pass plugin
structure, signature, Plugin Verifier, and installed-IDE acceptance against
IntelliJ IDEA 2026.2. The acceptance scenario uses only free-tier HTML and
platform LSP features; it does not require an Ultimate subscription.

Pannonico's canonical editor LSP is `pannonico-lsp.wasm`. This plugin executes
it through the repository-pinned, verified Wasmtime release and never resolves
a mutable latest runtime. Update the host table, acquisition contracts,
protocol/editor/host acceptance, and documentation together with any Wasmtime
pin. A native Pannonico LSP fallback requires a separately approved
architecture change.
