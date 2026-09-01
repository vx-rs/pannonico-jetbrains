# JetBrains release

The initial release is `0.5.0`. Later JetBrains-only changes increment the
JetBrains patch version without forcing unrelated tracks to use the same patch
number.

Pannonico supports only the current JetBrains platform generation. The initial
release uses `sinceBuild = 262` and `untilBuild = 262.*`.

When moving to a new generation, update the build range, IntelliJ Platform
dependency, LSP API, IntelliJ IDEA Plugin Verifier target, installed test, and
documentation together. Do not retain older-generation API compatibility
unless explicitly requested.

Every LSP release requires a new author-signed plugin ZIP:

```text
npm run release:build -- jetbrains <plugin-version> <lsp-version>
npm run release:jetbrains -- <plugin-version>
```

Candidate signing reads `PANNONICO_JETBRAINS_CERTIFICATE_CHAIN`,
`PANNONICO_JETBRAINS_PRIVATE_KEY`, and
`PANNONICO_JETBRAINS_PRIVATE_KEY_PASSWORD` from the operator environment. Never
commit these values. Upload the exact GitHub Release ZIP manually to Marketplace
and run `npm run release:verify -- jetbrains <plugin-version>` after approval.

The checked-in Gradle 9.1 wrapper requires JDK 25. Development acceptance uses
the same Starter/Driver scenario without signing:

```text
PANNONICO_LSP_MANIFEST=/absolute/path/to/manifest.json \
PANNONICO_TEST_WASMTIME=/absolute/path/to/wasmtime \
npx nx run pannonico-jetbrains:test-installed-dev
```

Starter downloads unified IntelliJ IDEA 2026.2 by default. When that exact
release is already installed, `PANNONICO_JETBRAINS_IDE_HOME` may name its
application root; the identical automated scenario and plugin build-range
check still apply. The test uses only free-tier HTML and platform LSP features;
it does not require an Ultimate subscription.

Final release acceptance consumes only the already author-signed ZIP and exact
local LSP/Wasmtime files; it does not rebuild, download, repair, or sign them.
A failure retains `failure.json`, stdout, stderr, and Gradle report locations
below `.local/test-results/jetbrains/runs/`; success removes its run directory.

Pannonico's canonical editor LSP is `pannonico-lsp.wasm`. This plugin executes
it through the repository-pinned, verified Wasmtime release and never resolves
a mutable latest runtime. Update the host table, acquisition contracts,
protocol/editor/host acceptance, and documentation together with any Wasmtime
pin. A native Pannonico LSP fallback requires a separately approved
architecture change.
