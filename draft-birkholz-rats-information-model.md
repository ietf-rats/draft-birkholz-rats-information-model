---
title: An Information Model for Assertions used in RATS
abbrev: IMARA
docname: draft-birkholz-rats-information-model-latest
stand_alone: true
ipr: trust200902
area: Security
wg: RATS Working Group
kw: Internet-Draft
cat: std
pi:
  toc: yes
  sortrefs: yes
  symrefs: yes

author:
- ins: H. Birkholz
  name: Henk Birkholz
  org: Fraunhofer SIT
  abbrev: Fraunhofer SIT
  email: henk.birkholz@sit.fraunhofer.de
  street: Rheinstrasse 75
  code: '64295'
  city: Darmstadt
  country: Germany
- ins: M. Eckel
  name: Michael Eckel
  org: Fraunhofer SIT
  abbrev: Fraunhofer SIT
  email: michael.eckel@sit.fraunhofer.de
  street: Rheinstrasse 75
  code: '64295'
  city: Darmstadt
  country: Germany

normative:
  RFC2119:
  RFC8342:
  I-D.birkholz-rats-architecture: rats-arch
  I-D.birkholz-rats-tuda: TUDA
  I-D.mandyam-rats-eat: EAT
  I-D.tschofenig-rats-psa-token: PSA-token
  I-D.birkholz-rats-basic-yang-module: rats-yang

informative:
  I-D-birkholz-rats-reference-interaction-model: rats-interaction
  I-D.richardson-rats-usecases: rats-usecases

--- abstract

This document defines a standardized information model (IM) for assertions that can be used in remote attestation procedures (RATS).
The information elements defined include attestation assertions which provide information about system components characteristics, and commonly used attributes and attribute structures used in protocols for remote attestation.

--- middle

# Introduction

Remote attestation procedures (RATS) are used to increase the trust in the trustworthiness of an attester.
This is typically accomplished by conveying attestation evidence from an attester to a verifier that is able to appraise the evidence.
The exact definitions of RATS roles, such as an attester or a verifier, are specified in the RATS architecture {{-rats-arch}}.
This document defines the common information elements (IE) that are able to express the characteristics of an attester. Ultimately, these IE can be used to compose attestation evidence (attestation assertions that are accompanied by a proof of their validity).

In general, RATS convey information elements that:

* enable the functionality of remote attestation protocols,
* are able to express assertions about an attester's composition, configuration, or operational state,
* represent the provenance of assertions, including entities that provide assertions on behalf of the attester, and
* compose a type of proof of validity with respect to other assertions, and that
* are either verifiable (via comparison with trusted reference values) or non-verifiable.

## Document Structure

Every information element listed is annotated with one or more of these attributes:

Protocol (P):

: This IE is used on a remote attestation protocol layer, typically on the control plane or as protocol-specific data plane content.

Hardware (H):

: This IE expresses characteristics about an attester's hardware components or the composition of its hardware components.

Software (S):

: This IE expresses characteristics about an attester's software components or their semantic relationship. The term software component -- in the scope of this document -- subsumes firmware, bootloader, BIOS/(U)EFI, and microcode.

Operational State (O):

: This IE is used to convey information about the combination of applied configuration and system state as defined in {{RFC8342}}.

Verifiable (V):

: This IE requires reference integrity measurements (RIM), compliance-policy, certification-path, or another type of trust-chain in order to be appraised appropriately by a verifier.

Additionally, every IE definition includes a reference to the source of its definition, if it is not specified in this document for the first time (which is the most likely case).
If a source of a definition is not a specification or (proposed) standard, but a draft, a web resource, or source that cannot be attribute with a DOI or ISSN, the following attribute is associated.

Unstable (U):

: The source of the definition of this IE may change in the future and is not considered to be stable at the time of publication of this document.

Information elements might reference other information elements or have to be associated in a set (with or without a specific order) in order to convey the intended meaning to a verifier. Reference to other IE inside this documents simply use their name as reference. In consequence, an IE can be a superstructure composed of other IE with its own name (and potentially additional definition text that defines its purpose and or usage).

The RATS Information Model allows for expressing a hierarchical taxonomy. If an IE is a specialisation of another IE, the last sentence in the definition includes a "This IE is a specialization of *IE NAME*".

The ordering of IE is in descending alphabetical order; independent of source or semantic relationship to other IE, or other types of hierarchy.

# RATS Information Elements

Assertion Selection:

: [P]

: A filter expression that enables the conveyance of a subset of all attestation assertions available to the attester, if requested by a verifier.

Attestation Evidence:

: [H, S, O, V]

A composite IE that must include at least an Authentication-Secret Identifier, an Attester Identity, and at least one Attestation Assertion.
Attestation Evidence is always signed via the Authentication Secret and thereby binds the listed information elements cryptographically.
Attestation Evidence can only be trusted by a verifier if it is associated with a trust anchor the verifier also trusts.

Attester Identifier:

: [P, O, V]

: A value associated or bound to a distinguishable attester that is intended to uniquely identify it, but is not directly associated with a trust anchor.
Additional Endorsement Documents can increase the level of confidence in an Attester Identifier.

Attester Identity:

: [P, S, V]

: A document about a distinguishable attester issued and signed by a third party.
If not cryptographically associated with a trust anchor directly or indirectly, this IE is a specialization of Attester Identifier.

Attestation Result:

: [P]

: A set of one or more values that are created by an appraisal action of a verifier.
Attestation Result is the most generic definition of the output of RATS and are typically consumed by relying parties.

Authentication-Secret Identifier:

: [O, V]

: An identifier that is associated with an authentication secret used to sign attestation evidence.

Endorsement Document:

: [P, H, S, V]

A document about the capabilities and functionality of one or more sub-components of a distinguishable attester issued and signed by a third party.
Endorsement Documents are intended to render Attestation Evidence trustworthy.
If not cryptographically associated with a trust anchor directly or indirectly, this IE is a specialization of System Component Identifier.

Nonce:

: [P]

: TBD

Origination:

: TBD

: TBD

: Reference {{-EAT}}

Universal Entity ID:

: [P, H, V]

: A unique identifier permanently associated with an individual manufactured entity / device, such as a mobile phone, a water meter, a Bluetooth speaker or a networked security camera.
This IE is intended to either identify an device or a submodule or subsystem.
It does not identify types, models or classes of devices.
It is akin to a serial number, though it does not have to be sequential.
This IE is a specialization of System Component Identifier.

: Reference {{-EAT}}

#  Security Considerations

Probably none

#  Acknowledgments

TBD

#  Change Log

Initial version -00

# Contributors

TBD

--- back
