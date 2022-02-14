
JSON-LD Credentials in ACA-Py
By design Hyperledger Aries is credential format agnostic. This means you can use it for any credential format, as long as an RFC is defined for the specific credential format. ACA-Py currently supports two types of credentials, Indy and JSON-LD credentials. This document describes how to use the latter by making use of W3C Verifiable Credentials using Linked Data Proofs.

Est-ce que cela veut dire que l'on doit implémenter un nouveau format de credential basé sur OCA pour la RFC-0013? Car si je comprends bien, le chema de base de OCA n'est pas un schéma indy. On ne peut pas l,exploiter directement.
