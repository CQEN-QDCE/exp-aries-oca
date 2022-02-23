
JSON-LD Credentials in ACA-Py
By design Hyperledger Aries is credential format agnostic. This means you can use it for any credential format, as long as an RFC is defined for the specific credential format. ACA-Py currently supports two types of credentials, Indy and JSON-LD credentials. This document describes how to use the latter by making use of W3C Verifiable Credentials using Linked Data Proofs.

Est-ce que cela veut dire que l'on doit implémenter un nouveau format de credential basé sur OCA pour la RFC-0013? Car si je comprends bien, le chema de base de OCA n'est pas un schéma indy. On ne peut pas l,exploiter directement.

https://www.youtube.com/watch?v=LC0OXAir3Qw

AnonCreds Schema Background
Credential Metadata
The AnonCreds verifiable credential schema as defined in the Open Source Hyperledger Indy implementation consists of a flat list of schema claims. The presentation of claims from one or more AnonCreds verifiable credentials conveys those claims and minimal metadata about the verifiable credential. The following is determined from the provided metadata:



An identifier for the issuer of the credential.

Proof that the credential was issued to the holder/prover.

Cryptographic signatures on the claims to provide evidence of tampering, if any.

A resolvable address from which to find the public keys needed to verify the signatures.

Proof that the credential has not been revoked by the issuer.

A resolvable address from which to get cryptographic data necessary to verify non-revocation.



Note that the list does not automatically include information about the credential such as when it was issued and when it expires. If that type of information is appropriate for a credential, it must be included in the claims.

Claims Encoding
AnonCreds claims are provided in both a raw (plaintext) form and encoded into 32-bit integers. It is the encoded value that is signed and verified. The current rules for encoding the raw values in the current Aries AnonCreds implementations is quite simple, as detailed here and summarized as:



All integers are left as 32-bit integers.

All strings are SHA256 hashed into 32-bit integers



Thus, while the format of the raw claims may be defined in the Schema, the encoded values are either integers or hashes of strings.

Date Handling
While it is usual to encode dates in a standard format (such as ISO-8601) in credentials, that is not particularly useful when using AnonCreds in general, and in the Verified Person credential in particular. That is because storing the data in that format is putting it into a string, and in AnonCreds strings are encoded as hashes that are not sortable. As a result, such dates cannot be used in zero knowledge proof (ZKP) “predicates”, such as “the holder equal to or older than 19 years.” The convention with AnonCreds is to store dates as the integer value of “YYYYMMDD.” so that they are both sortable (and so useful in predicates) and familiar looking to holders. For example, January 1, 2022 is issued in a claim as the integer 20220101.



This is for a sequence of reasons:



The Verified Person “Date of Birth” field is a piece of PII that we would like the holder to be able to not disclose whenever possible.

Common date fields in verifiable credentials such as “Date Issued” and “Expiry Date” serve as corelatable identifiers in many cases. If multiple verifiers collect that information from Holders, they likely have a more or less unique identifier for either the credential or the person. Again, we would like to allow the holder not to disclose that information.

To allow dates to be checked (e.g. an “Older than” check, or a “Credential not expired” check) in AnonCreds, zero knowledge proof (ZKPs) predicates can be used such that a true or false value is returned without disclosing the value of the claim used in an expression. For example, the predicates:

date_of_birth < today()-years(19)

exp > today()

Predicates operate on the encoded value, and the claims must be sortable to be compared in an expression.

To prevent the date from being treated as a string according to the AnonCreds encoding, it must be issued as a 32-bit integer.

The integer format for the date (e.g. 20220101) is both sortable and understandable if presented as a plain number to a Holder (e.g. “Date of Birth: 19940713”) would look a little odd, but be understandable to most people in Canada.

Note that if a Wallet knew of the format of the claim, it could present the data in an even friendlier format (e.g. “Date of Birth: June 13, 1994”).



This convention is outlined in Aries RFC 0492 about AnonCreds handling, which also suggest that the name of the claim holding such a date should have the suffix “_dateint.” Note that this convention does NOT apply to or work for datetime fields.
