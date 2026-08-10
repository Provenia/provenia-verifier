# Provenia verifier reference package

This directory is the initial reference package for local verification of a Provenia dossier. It documents the verification contract currently implemented by Provenia Issue #73 and records the active production public key.

No GitHub release or Zenodo DOI exists as part of this package. Future GitHub and Zenodo publication references are pending.

Start with [VERIFICATION_METHOD.md](VERIFICATION_METHOD.md) for the operational sequence and [VERIFICATION_SPECIFICATION.md](VERIFICATION_SPECIFICATION.md) for the contract. The original Record files are compared locally against their recorded SHA-256 values and are never uploaded.

The ZIP file is only a distribution container for the official verification artifacts, `Dossier.json` and `Dossier.pdf`; ZIP packaging itself is not a cryptographic proof.

The trusted key is [public-keys/provenia-prod-2026-01.pem](public-keys/provenia-prod-2026-01.pem), with history in [key-history.json](key-history.json).
