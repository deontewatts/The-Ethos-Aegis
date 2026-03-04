# Security Policy
## The Security Vault: Protecting the Defender

The `ethos_aegis.security` module addresses a threat class that none of the SentinelCells can defend against: what if the defense code itself is tampered with? An attacker who can modify `aegis.py` to remove a TaintBeacon semantic cluster, or weaken a VanguardProbe sigil threshold, has compromised the immune system from within — the digital equivalent of autoimmune disease.

The IntegrityVerifier pre-computes SHA-256 fingerprints of every source file at initialization time and stores them as reference hashes. Before deployment, `verify()` recomputes every fingerprint and compares against the reference. Any mismatch is a critical security event.

The AuditLedger implements a SHA-256 hash chain analogous in structure to a blockchain, but without the distributed consensus overhead: each entry's content hash covers all its fields including the previous entry's hash, so altering any entry breaks the chain at that point and at every subsequent point. The `verify_chain()` walk detects exactly which entry was tampered with. The critical privacy-preserving design choice is that the ledger stores SHA-256 hashes of payload text, not the text itself — the log proves that a specific payload was adjudicated without retaining potentially sensitive content.
