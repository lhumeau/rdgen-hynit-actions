# HYNIT RDGen build workflows

This workflow-only repository builds HYNIT Remote Support desktop clients for Windows x64, macOS Intel/Apple Silicon, and Linux x64. The application and reviewed source fork live at https://github.com/lhumeau/rdgen-hynit.

Repository Actions secrets required by the workflows:

- `GENURL=https://rdgen.hynit.com`
- `ZIP_PASSWORD` matching the RDGen server's local `.env`
- `RDGEN_CALLBACK_TOKEN` matching the RDGen server's local `.env`
- `RDGEN_ZIP_URL`, a temporary presigned GET URL for the encrypted config archive in Contabo S3; remove it after the three setup jobs have downloaded the archive.

The RDGen server supplies the client configuration and dispatches these workflows. The workflows upload installer outputs as short-lived GitHub artifacts instead of posting through the Cloudflare-protected RDGen hostname. The operator downloads and publishes the verified installers to Contabo S3 bucket `software` using Agency presigned PUTs.

The workflows and local actions are based on `bryangerlach/rdgen` and are licensed under GPL-3.0; see `LICENSE`.
