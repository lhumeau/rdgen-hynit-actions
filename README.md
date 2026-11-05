# HYNIT RDGen build workflows

This workflow-only repository builds HYNIT Remote Support desktop clients for Windows x64, macOS Intel/Apple Silicon, and Linux x64. The application and reviewed source fork live at https://github.com/lhumeau/rdgen-hynit.

Repository Actions secrets required by the workflows:

- `GENURL=https://rdgen.hynit.com`
- `ZIP_PASSWORD` matching the RDGen server's local `.env`
- `RDGEN_CALLBACK_TOKEN` matching the RDGen server's local `.env`

The RDGen server supplies the client configuration and dispatches these workflows. Build outputs are sent back to RDGen; the operator publishes the verified installers to Contabo S3 bucket `software`.

The workflows and local actions are based on `bryangerlach/rdgen` and are licensed under GPL-3.0; see `LICENSE`.
