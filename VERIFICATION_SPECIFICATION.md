# Verification specification

## Evidence and algorithms

- `Dossier.json` is canonically serialized by the current Provenia generator after removing its `signature` member, then signed with Ed25519. The signature is base64-encoded.
- The embedded public key is PEM SubjectPublicKeyInfo. Its trust fingerprint is SHA-256 over the DER SubjectPublicKeyInfo, represented as lowercase hexadecimal.
- `Dossier.pdf` is the complete signed PDF. Its recorded digest is SHA-256. The PDF must contain exactly one intact and valid PAdES signature; Provenia produces PAdES with an ICP-Brasil e-CNPJ certificate.
- Public-key trust requires the embedded key and fingerprint to agree and the key ID/fingerprint to match a key in the Provenia registry. A `RETIRED` key remains eligible for successful trust validation when its `key_id` exists in the trusted registry, its fingerprint matches, and it is not `REVOKED`; retired keys remain published so historical Dossiers can continue to be verified. A revoked key fails trust; an unavailable or unmatched registry entry is partial.
- RFC3161 evidence is checked per record against that record's file hash and nonce. It is evidence for the record, not an independent date for the institutional JSON signature.
- Record-chain verification requires one-based, unique sequence numbers, unique UUIDs, and valid backward `based_on` references.

## Results

`VERIFIED` means every produced check passed. `PARTIAL` means no check failed but at least one check could not be fully established (for example incomplete RFC3161 evidence or unavailable key trust). `FAILED` means at least one check failed, including malformed package/manifest, invalid Ed25519 signature, mismatched trusted key, invalid PAdES/PDF hash, invalid RFC3161 evidence, or broken record chain.

## Packaging and local records

ZIP is only a distribution container for verification artifacts; it is not itself an attestation. The verifier must compare original Record files locally with the `file_hash` values in `Dossier.json`. Those original files are never uploaded.

The published `v1.0.0` reference package is archived at `https://doi.org/10.5281/zenodo.21877417`. The GitHub release and Zenodo archive are publication references, not cryptographic trust anchors.
