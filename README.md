# Provenia verifier reference package

This directory is the reference package for local verification of a Provenia dossier. It documents the verification contract in [VERIFICATION_SPECIFICATION.md](VERIFICATION_SPECIFICATION.md) and records the active production public key.

The current published reference version is [`v1.0.0`](https://github.com/Provenia/provenia-verifier/releases/tag/v1.0.0). It is archived on Zenodo at [doi:10.5281/zenodo.21877417](https://doi.org/10.5281/zenodo.21877417).

Start with [VERIFICATION_METHOD.md](VERIFICATION_METHOD.md) for the operational sequence and [VERIFICATION_SPECIFICATION.md](VERIFICATION_SPECIFICATION.md) for the contract. The original Record files are compared locally against their recorded SHA-256 values and are never uploaded.

The ZIP file is only a distribution container for the official verification artifacts, `Dossier.json` and `Dossier.pdf`; ZIP packaging itself is not a cryptographic proof.

The trusted key is [public-keys/provenia-prod-2026-01.pem](public-keys/provenia-prod-2026-01.pem), with history in [key-history.json](key-history.json).

## License

The documentation, verification specification, verification method, public-key registry metadata, and other non-software materials in this repository are licensed under the [Creative Commons Attribution 4.0 International License](LICENSE) (CC BY 4.0), unless otherwise noted.

This license does not grant rights to Provenia trademarks, brand identity, logos, or other branding elements.

No executable software is currently distributed in this repository. If executable software is added in the future, it will be licensed separately under an appropriate software license.
