# PP-SPEC-009 · ProofStamp™ Certification Criteria

**Document ID:** PP-SPEC-009  
**Version:** 0.1 - Draft  
**Status:** Draft  
**License:** CC BY 4.0  
**Maintained by:** Proof Economy™ Standards Alliance (PESA)  
**Repository:** https://github.com/proofprotocol/proofstamp-criteria  
**Published:** 2026-07-13  

---

## Abstract

This specification defines the criteria a product or agent must satisfy to earn ProofStamp™ certification. ProofStamp™ is a certification mark owned by Nebulonium, Inc. (HACKERverse). It is not software. It cannot be forked, replicated, or self-issued.

ProofStamp™ certifies that an independent party reviewed a ProofBundle™, confirmed the methodology was sound, and staked their mark on the result.

The stamp is earned. Not minted. Not self-declared.

---

## Status of This Document

Draft. Subject to change before v1.0.

---

## Table of Contents

1. [What ProofStamp™ Is](#1-what-proofstamp-is)
2. [What ProofStamp™ Is Not](#2-what-proofstamp-is-not)
3. [Certification Requirements](#3-certification-requirements)
4. [Certification Process](#4-certification-process)
5. [ProofStamp™ Token](#5-proofstamp-token)
6. [Renewal](#6-renewal)
7. [Revocation](#7-revocation)
8. [Enterprise ProofServer Deployments](#8-enterprise-proofserver-deployments)
9. [Conformance](#9-conformance)
10. [Authors](#10-authors)

---

## 1. What ProofStamp™ Is

ProofStamp™ is a certification mark. It is the legal and institutional signal that a product or agent has been independently evaluated under the Proof Protocol™ and met the certification criteria defined in this specification.

ProofStamp™ answers the question every buyer, auditor, and regulator needs answered: who watched the watcher?

The answer is structural. The certifying authority operates outside the trust boundary of the System Under Test's operator, and its compensation does not vary with the verdict. It does not sell products in the category it certifies.

Independence here is a structural position, not a claim of disinterest. Where the certifying authority holds a commercial relationship with the subject, contributed to authoring the conformance criteria, or holds more than one role in a given run, those facts MUST be disclosed in the certification record. Disclosure does not create independence. It makes the residual visible.

That structural position cannot be replicated by any party that sells products in the category it certifies, nor by any body funded by the vendors it evaluates.

---

## 2. What ProofStamp™ Is Not

ProofStamp™ is not:

- A software license
- A self-certification mechanism
- A badge issued on the basis of self-attestation
- A conformance claim that can be made without a corresponding ProofBundle™
- A permanent certification that survives product version changes without renewal

A vendor may not display the ProofStamp™ mark without a current valid ProofStamp™ authorization token issued by HACKERverse. Unauthorized use of the ProofStamp™ mark is a trademark violation.

---

## 3. Certification Requirements

A product or agent must satisfy all of the following to earn ProofStamp™ certification:

**3.1 Valid ProofBundle™**
A conformant ProofBundle™ submitted to ProofRegister™ per PP-SPEC-003 and PP-SPEC-004.

**3.2 Independent Witness**
The benchmark run must have been witnessed by a qualified independent witness per PP-SPEC-005. The witness attestation record must be included in the ProofBundle™.

**3.3 NIST Beacon Pre-Execution Commitment**
The test parameters must have been committed to a NIST Beacon pulse before execution began per PP-SPEC-008.

**3.4 Published Scores**
The Report must carry `proof: true` and must publish the Containment Score and the Detection Score together, with the full case classification breakdown, the detected count, and all declared exclusions.

There is no minimum score. ProofStamp™ certifies that the measurement was independently witnessed and pre-committed, not that the subject performed well. A certified Report carrying a low score is as valid as one carrying a high score, and both MUST be registered. Withholding certification from poor results would produce a registry containing only favourable outcomes, which is vendor benchmarking with cryptography applied.

Buyers set their own thresholds. The certifying authority does not.

**3.5 Full Threat Category Coverage**
The benchmark run must cover the full enumerated threat category set for the domain without undisclosed exclusions per PP-SPEC-006.

**3.6 Verdict-Invariant Compensation**
The certifying authority's compensation MUST be identical whether the Report carries proof or not, and regardless of any score it carries. A fixed fee for certification is permitted and MUST be disclosed. Equity, resale margin, referral fees, success-contingent pricing, or any benefit varying with the outcome disqualifies the authority from certifying that subject.

A commercial relationship does not disqualify. A commercial relationship whose value depends on the result does.

**3.7 Methodology Review**
The certifying authority must review and approve the execution methodology before issuing the stamp. Where the certifying authority also acted as Corpus Authority, Witness, or Scoring Authority for the run, each role held MUST be declared in the certification record.

---

## 4. Certification Process

1. Vendor submits a ProofBundle™ to ProofRegister™ via the PP-SPEC-004 API
2. Vendor requests ProofStamp™ certification review at proofstamp.io
3. HACKERverse reviews the ProofBundle™ for conformance with PP-SPEC-003 through PP-SPEC-008
4. HACKERverse confirms witness eligibility and attestation
5. HACKERverse issues a ProofStamp™ authorization token if all criteria are met
6. The ProofStamp™ token is added to the ProofBundle™ as `proofstamp.json`
7. The ProofRecord in ProofRegister™ is updated with the ProofStamp™ ID

---

## 5. ProofStamp™ Token

```json
{
  "proofstamp_id": "PS-YYYY-NNNNN",
  "product_name": "string",
  "product_version": "string",
  "vendor": "string",
  "proof_record_id": "PR-YYYY-NNNNN",
  "issued_at": "RFC 3339 UTC",
  "expires_at": "RFC 3339 UTC",
  "pes_score": 0.0,
  "benchmark_name": "string",
  "benchmark_version": "string",
  "authorization_signature": "Ed25519 hex signature",
  "issuer_public_key": "hex",
  "proofstamp_uri": "https://proofstamp.io/verify/PS-YYYY-NNNNN"
}
```

The `authorization_signature` is an Ed25519 signature by HACKERverse over the canonical JSON of this token excluding the signature field itself. Any party can verify it against the `issuer_public_key` published at proofstamp.io.

---

## 6. Renewal

ProofStamp™ certification is valid for 12 months from the `issued_at` date or until a new major version of the certified product is released, whichever comes first.

Renewal requires a new benchmark run and new ProofBundle™ submission. A renewed certification supersedes but does not revoke the prior certification record.

---

## 7. Revocation

HACKERverse may revoke a ProofStamp™ certification if:

- Material misrepresentation was discovered in the ProofBundle™ or witness attestation
- The certified product version is no longer in active use or support
- The vendor requests revocation
- Evidence emerges that the run was conducted outside the declared posture

Revocation sets the ProofRecord status to `revoked` in ProofRegister™. The ProofStamp™ token becomes invalid. The vendor must remove the ProofStamp™ mark from all materials within 30 days of revocation notice.

Revocation is permanent and public. The revocation reason is recorded in ProofRegister™.

---

## 8. Enterprise ProofServer Deployments

Enterprise organizations running ProofServer internally may submit bundles to ProofRegister™ and request ProofStamp™ certification for their internal deployments. Certification criteria are identical.

ProofServer software may be open source. ProofStamp™ authorization is always issued by HACKERverse. A ProofServer fork cannot issue ProofStamp™. A ProofServer deployment that has not been certified by HACKERverse may not display the ProofStamp™ mark.

---

## 9. Conformance

There is no self-conformance mechanism for ProofStamp™. Conformance is determined solely by HACKERverse review. A product that meets all technical criteria in Section 3 but has not received a ProofStamp™ authorization token from HACKERverse is not ProofStamp™ certified.

---

## 10. Authors

Craig Ellrod, Founder & CEO, Nebulonium, Inc. (d/b/a HACKERverse)  
Castle Rock, Colorado  
2026-07-13

---

*CC BY 4.0 - Attribution to Craig Ellrod / Nebulonium, Inc. required.*
