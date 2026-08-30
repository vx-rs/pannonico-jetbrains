# JetBrains release

The initial release is `0.5.0`. Later JetBrains-only changes increment the
JetBrains patch version without forcing unrelated tracks to use the same patch
number.

Pannonico supports only the current JetBrains platform generation. The initial
release uses `sinceBuild = 262` and `untilBuild = 262.*`.

When moving to a new generation, update the build range, IntelliJ Platform
dependency, LSP API, Plugin Verifier matrix, installed tests, and documentation
together. Do not retain older-generation API compatibility unless explicitly
requested.

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
