# Verification method

The current Provenia verification sequence is:

1. Open the submitted ZIP locally. Require exactly the supported `Dossier.json` and `Dossier.pdf` members (optionally under one directory), with no duplicate, encrypted, unsafe-path, oversized, or excessive-compression entries. ZIP is only a distribution container.
2. Decode and validate `Dossier.json`, including schema metadata, dossier metadata, PDF filename/hash fields, records, and signature fields.
3. Remove only the `signature` member and reproduce Provenia's canonical JSON serialization. Verify the base64 signature with Ed25519.
4. Derive the public-key fingerprint from the embedded PEM, then validate institutional trust using that fingerprint together with the key ID against the trusted Provenia registry. A `RETIRED` key remains eligible for successful trust validation when its `key_id` exists in the trusted registry, its fingerprint matches, and it is not `REVOKED`; retired keys remain published so historical Dossiers can continue to be verified. The current production key is active and recorded in this package.
5. SHA-256 is the required PDF hash algorithm: compute SHA-256 over the complete final signed `Dossier.pdf` bytes and compare it with `dossier.pdf_hash`; an unsupported or non-SHA-256 declared algorithm causes PDF verification to fail. Require one valid intact PAdES signature.
6. Validate record sequence numbers, UUID uniqueness, and each `based_on` reference: referenced records must exist, be earlier, and have the stated sequence number.
7. For records carrying external timestamp evidence, decode and verify the RFC3161 response against the record file hash and nonce. Missing/incomplete evidence is partial; invalid evidence fails.

Original Record files are compared locally by hashing the files supplied by the verifier against each record's `file_hash`. They are never uploaded by this verification contract.

Overall result semantics are failure-dominant: `FAILED` if any check fails; otherwise `PARTIAL` if any check is partial; otherwise `VERIFIED` when all checks pass. A dossier with no RFC3161 attestations passes that check as “no attestations are present”; this does not create a timestamp proof.
