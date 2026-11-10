# HYNIT RDGen build workflows

This workflow-only repository builds HYNIT Remote Support desktop clients for Windows x64, macOS Intel/Apple Silicon, and Linux x64. The application and reviewed source fork live at https://github.com/lhumeau/rdgen-hynit.

Repository Actions secrets required by the workflows:

- `GENURL=https://rdgen.hynit.com`
- `ZIP_PASSWORD` matching the RDGen server's local `.env`
- `RDGEN_CALLBACK_TOKEN` matching the RDGen server's local `.env`

Optional fallback: `RDGEN_ZIP_URL` can hold a temporary presigned GET URL for the encrypted config archive in Contabo S3 if Cloudflare blocks GitHub's RDGen callback request. Remove it after the setup jobs have downloaded the archive.

The RDGen server supplies the client configuration and dispatches these workflows. The workflows upload installer outputs as short-lived GitHub artifacts instead of posting through the Cloudflare-protected RDGen hostname. The operator downloads and publishes the verified installers to Contabo S3 bucket `software` using Agency presigned PUTs.

The current HYNIT mark and app icon, sourced from Lotería’s active `hynit-mark.svg`, live in `branding/`. The Windows, macOS, and Linux workflows embed the current local HYNIT mark and icon, so build runners do not fetch logo images from RDGen during compilation.

The Windows and Linux workflows bundle the upstream `mfx_dispatch` cstdint patch in `patches/` and seed vcpkg's download cache with its verified SHA-512. This avoids repeated GitHub HTTP 429 responses for that fixed upstream patch without disabling hardware-codec support.

The workflows and local actions are based on `bryangerlach/rdgen` and are licensed under GPL-3.0; see `LICENSE`.
