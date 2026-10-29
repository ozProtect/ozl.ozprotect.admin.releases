# ozProtect Admin releases

Binary distribution and signed update feed for the ozProtect desktop panel.
The application source and frontend submodule are private; this repository holds
only release infrastructure, a source revision/version request, and binary assets.

Windows packages:

- `*-setup.exe`: per-user installer.
- `*-portable.exe`: portable application, no installation required.
- `update.json` and `update.json.sig`: exact-byte Ed25519-signed update metadata.

Updates require a matching pinned public key, package size and SHA-512. Installation
asks before closing the application. The initial Windows packages are not
Authenticode-signed; the Ed25519 update signature is separate from OS code signing.

The private source repository's `prod` workflow sends only its SHA and version.
The builder checks the current private `prod` head against that request, then
publishes binaries with this repository's own short-lived workflow token.
The GitHub App installation is restricted to the two desktop wrapper repositories;
checkout tokens are read-only and source-to-release metadata tokens are write-only
to this repository. No personal GitHub token or frontend checkout is published.

macOS Intel/Apple Silicon and Linux x64/ARM64 builds are prepared as an opt-in
workflow matrix. Their native acceptance and updater installation are future work;
they are not part of the initial public Windows update feed.
