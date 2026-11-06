# JetBrains release

## Release history

### 0.7.2

- Replace the path hook marked internal in IntelliJ IDEA 2026.3 with the public
  URI hook available on the initial 262 baseline. Encode filename characters
  as URI path data and preserve reverse navigation through the WASI preopen.
- Complete pending per-file VFS writes before handing file URIs to the external
  language server, so saved diagnostics use the completed disk content.
- Select Pannonico LSP 0.7.1, which preserves saved compiler diagnostics after
  equivalent or delayed full-text synchronization.
- Verify fixed IntelliJ IDEA 2026.2.4 (262.11879.100) and 2026.3 (263.7307.200)
  targets, retaining the 262 minimum, open upper range and Wasmtime 48.0.1.

### 0.7.1

- Preserve IntelliJ Platform build 262 as the minimum and remove the upper
  host-version bound. Newer IDE versions are eligible on a best-effort basis.
- Disable Gradle's default upper bound in checked-in configuration so every
  build preserves the open-ended range without an operator flag.
- Retain Pannonico LSP 0.7.0 and the verified Wasmtime 48.0.1 runtime.

### 0.7.0

- Select Pannonico LSP 0.7.0, which keeps idle WASI stdin sessions open.
- Target IntelliJ Platform 2026.2 with build range `262` through `262.*`.
- Include the registered completion typed handler in release builds so the IDE
  can load it and preserve partial-path completion triggers.

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

Pannonico preserves the initial IntelliJ Platform build 262 minimum and sets no
upper bound. Newer minor, patch and major IDE versions are eligible on a
best-effort basis. The maintained IntelliJ IDEA 2026.2 host is the tested
baseline, not an installation ceiling. Earlier hosts are not supported.

Gradle defaults `until-build` to the selected platform branch even when the
source descriptor omits it. The checked-in `untilBuild = provider { null }`
disables that default for every build; the operator supplies no compatibility
override. When an observed IDE incompatibility needs an update, review the API,
dependency, verifier target, installed test and documentation together.

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
IntelliJ IDEA 2026.2.4 (262.11879.100) and 2026.3 (263.7307.200). These fixed
verification targets do not cap installation eligibility. Installed acceptance
uses the existing `PANNONICO_JETBRAINS_IDE_HOME` override for each selected host
and exercises URI-sensitive filenames, definition navigation and saved compiler
diagnostic recovery. The acceptance scenario uses only free-tier HTML and
platform LSP features; it does not require an Ultimate subscription.

The completion-prefix override and per-file VFS flush use public experimental
platform APIs, which Plugin Verifier can report. The flush completes pending
writes before the external language server reads saved project files.

Pannonico's canonical editor LSP is `pannonico-lsp.wasm`. This plugin executes
it through the repository-pinned, verified Wasmtime release and never resolves
a mutable latest runtime. Update the host table, acquisition contracts,
protocol/editor/host acceptance, and documentation together with any Wasmtime
pin. A native Pannonico LSP fallback requires a separately approved
architecture change.
