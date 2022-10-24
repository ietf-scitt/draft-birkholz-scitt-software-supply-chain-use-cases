---
v: 3

title: Detailed Software Supply Chain Uses Case for SCITT
abbrev: SCITT SW Supply Chain
docname: draft-birkholz-scitt-software-supply-chain-use-cases-latest
keyword: Internet-Draft
cat: info
stream: IETF

venue:
  group: SCITT
  mail: scitt@ietf.org
  github: ietf-scitt/draft-birkholz-scitt-software-supply-chain-use-cases

pi: [toc, sortrefs, symrefs, compact, comments]

author:
  - ins: H. Birkholz
    name: Henk Birkholz
    org: Fraunhofer Institute for Secure Information Technology
    abbrev: Fraunhofer SIT
    email: henk.birkholz@sit.fraunhofer.de
    street: Rheinstrasse 75
    code: '64295'
    city: Darmstadt
    country: Germany
  - ins: D. Brooks
    name: Dick Brooks
    org: REA
    email: dick@reliableenergyanalytics.com
  - ins: R. Martin
    name: Robert Martin
    org: MITRE
    email: ramartin@mitre.org
  - ins: B. Knight
    name: Brian Knight
    org: Microsoft
    email: brianknight@microsoft.com
  - ins: Y. Deshpande
    name: Yogesh Deshpande
    org: ARM
    email: Yogesh.Deshpande@arm.com
    
normative:

informative:

--- abstract

Generalized Software Supply Chain Use Case Descriptions

--- middle

# Introduction {#intro}

Modern software applications are an intricate mix of first-party and third-party code, development practices and tools, deployment methods and infrastructure, and interfaces and protocols.
The software supply chain comprises all elements associated with an application's design, development, deployment, and maintenance throughout its entire lifecycle.
The complexity of software coupled with a lack of lifecycle visibility increases the risks associated with system attack surface and the number of cyber threats capable of harmful impacts, such as exfiltration of data, disruption of operations, and loss of reputation, intellectual property, and financial assets.
There is a need for a platform architecture that will allow consumers to ascertain that suppliers maintained appropriate security practices without requiring access to proprietary intellectual property.
SCITT-enabled products and analytics solutions will assist in managing compliance and assessing risk to help prevent and detect supply chain attacks across the entire software lifecycle while prioritizing data privacy.

[^abs2-]

[^abs2-]: Insert more detail on the development and deployment flows, threat landscape, and notional artifacts that allow security/compliance risk assessment.

## Terminology {#terms}

{::boilerplate bcp14-tagged}

# Generic Problem Statement

As illustrated in {{lifecycle-threats}}, a supply chain attack may leverage one or more lifecycle stages and directly or indirectly target the component.

~~~~
threat chain diagram here
~~~~
{: #lifecycle-threats title="Example Lifecycle Threats"}

[^status]

[^status]:
    Text on notional artifacts to be collected and to underscore the payload agnostic concept needed.
    Also insert notatonal artifacts table here.

# Notational Implementation

TBD

~~~~
deployment chain diagram here
~~~~
{: #deployment-chain title="Deployment Example of SCITT in Software Development"}

# Software Supply Chain Use Cases
SCITT fundamental architecture emphasizes heavily on introducing transparency and accountability to the entire steps involved in software delivery. With the advancement of Software Bill of Materials (SBOM) as a standard practice for managing software deliveries the below use case will take SBOM as an example to illustrate how a SCITT based system can augment security built using SBOMs.

## Software Bill of Material

Micro Coding Wizards (MCW) is a small, fictional, software development company providing software solutions to help manage a fleet of electric vehicles (EV) for corporations.
MCW’s software solution, MCWManager, is an asset management platform specifically designed to manage electric vehicle fleets.
MCWManager tracks usage, charge level, range, and other important characteristics of each EV in the fleet.
The US Department of the Interior (DOI), a government agency has expressed interest in licensing the MCWManager software to manage a fleet of 20 Electric Vehicles, spread across the Western Region, which includes States west of the Rocky Mountains.

MCW has been informed by DOI that their software will be subject to Cybersecurity Executive Order (EO) 14028 recommendations from NIST and will need to supply "Software Bill of Materials" (SBOM) and a "Vulnerability Disclosure Report" (VDR) NIST attestation to the DOI prior to procurement.

### Producer (MCW) Actions

A software producer, in this case MCW, creates a digitally signed SBOM, listing all the components contained in the final “distribution package” which a software consumer downloads in preparation for deployment within their digital ecosystem.
The following steps are performed by the Software Producer:

1. Create the “final SBOM” listing all the components contained in the final distribution package of a software product, which the customer will install into their environment.
The SBOM must follow NTIA minimum elements for SBOM’s and other NTIA and NIST recommendations for SBOM, to meet Executive Order 14028 and OMB M-22-18 requirements.
(Co)SWID, SPDX or CycloneDX SBOM formats are acceptable for this artifact. 
2. The encoding of SBOM is specific to the protocol in question.
3. Makes a claim to establish its own identity as a producer of the overall SBOM.
4. The issuer in certain situations can make further claims (example claims that relate to steps that might assist independent building of the software components, to arrive at the final deliverable).
5. Once all the claim construction is complete, make a CBOR data payload of all the claims.
6. Signs the payload using SCITT recommended signing scheme. For now this will be COSE signing.
7. Submits the COSE signed object to the transparent registry.
8. Receives the return receipts (A COSE Countersignature object, containing the inclusion proofs, the original COSE payload and a signature from the transparency service).
9. Producer would then ship the software along with the return receipts to the Software Consumer.

### Consumer Actions

A software consumer, in this case DOI, receives the software deliverable along with return receipts from the Producer.

1. The Consumer may choose to verify that the received software specific claims are indeed present in the Transparency Service.
2. It will decode the return receipts to get the inclusion proof.
3. Using inclusion proofs it will cyrpotgraphically evaluate the presence of Supply Chain Artifacts (including SBOM) in the Transparency Service.
4. It will decode the CBOR Payload to get the SBOM and other claims made by the issuer.
5. It may do additional verification to check that the identity claim value matches the identity of the issuer from where it received the software or the trust chain linking to the issuer.
6. A format aware consumer can decode the SBOM contents and do the SBOM specific verification steps to further augment the trustworthiness of the received deliverable.
7. The consumer can decode other claims to establish augmented trust on the received software. for example decode the specific claim to get the required instructions to build the software it has received. This way it can compare the computed hash for the binary compiled locally against the received hash from SCITT registry. Any mis-match can be reported as an inconsistency.


#### SBOM specific actions
1. Verify the digital signature over the SBOM artifact and identify the signing key used to sign the SBOM, referred to as the SKID (Secret Key ID), assuming the signature is verified successfully.
2. Can perform risk assessment of the SBOM by performing a vulnerability search for each SBOM component, identifying any CVE's that are reported.


~~~~
deployment scenario diagram here
~~~~
{: #implement-scenario title="Potential SCITT Implementation Scenario"}

## Vulnerability Disclosure Report

MCW has been informed by DOI that their software will be subject to Cybersecurity Executive Order (EO) 14028 recommendations from NIST and will need to supply "Software Bill of Materials" (SBOM) and a "Vulnerability Disclosure Report" (VDR) NIST attestation to the DOI prior to procurement.

### Producer (MCW) Actions

A software producer, in this case MCW, participates in a Vulnerability Disclosure Program, and generates a Vulnerability Disclosure Report listing all the known vulnerabilities and mitigations, which a software consumer downloads in preparation for deployment within their digital ecosystem.
The following steps are performed by the Software Producer:

1. Participate in a Vulnerability Disclosure program.
2. Generate a Vulnerability Disclosure Report (VDR) listing all the known vulnerabilities and mitigation plans to meet Executive Order 14028 and OMB M-22-18 requirements.
3. Digitally sign the VDR artifact.
4. Place the VDR and digital signature artifacts within an access-controlled location, i.e., a customer portal, and provide the end consumer with a link to these artifacts for downloading to the customers environment. 

### Consumer Actions

A software consumer, in this case DOI, obtains a digitally signed VDR artifact from a software vendor, which initiates the following risk assessment process:

1. Produce a SHA-256 hash value for the VDR artifact.
2. Verify the digital signature over the VDR artifact and identify the signing key used to sign the VDR, referred to as the SKID (Secret Key ID), assuming the signature is verified successfully.
3. Submit an inquiry to a trusted SCITT Registry requesting confirmation that a trust declaration is present in the registry for the combination of SHA-256 hash value and SKID associated with the SBOM.
4. Consumer checks SBOM against NIST NVD. If vulnerabilities have been reported within NVD and not in the producer provided VDR, then raise an issue with the producer for report accuracy.
5. If a trust declaration is on file with the SCITT trusted registry then continue with the risk assessment, otherwise inform the consumer that the VDR hash and SKID combination are not registered, and the risk assessment ceases.
6. Continue with the risk assessment by performing a vulnerability search for each SBOM component, identifying any CVE’s that are reported.

## NIST self-attestation: SSDF Framework

Consistent with the NIST Guidance and by the timelines identified below, agencies are required to obtain a self-attestation from the software producer before using the software.

### Producer (MCW) Actions

An acceptable self-attestation must include the following minimum requirements:

1. The software producer's name.
2. A description of which product or products the statement refers to (preferably focused at the company or product line level and inclusive of all unclassified products sold to Federal agencies).
3. A statement attesting that the software producer follows secure development practices and tasks that are itemized in the standard self-attestation form.
4. Self-attestation is the minimum level required; however, agencies may make risk-based determinations that a third-party assessment is required due to the criticality of the service or product that is being acquired, as defined in M-21-30.

### Consumer Actions

TBD




--- back

<!--
Contributors
============
{: numbered="no"}

Add reference to [TIME] once available.

Ben Gamari suggested being able to use decimally scaled fractional
seconds in CBOR time.
 -->

<!--
Acknowledgements
================
{: numbered="false"}
-->

<!--  LocalWords:  SCIIT uscase SBOM NIST
 -->

# TODO List

* Promotion Scenario: '3rd party lab validates the detail instead of their own test'
* Endorsement Scenario: Audit downstream independent of issuer and provide an endorsement
* CI/CD SCITT interaction - Create a model before talking to Github (Statements about SW could be listed. Policy management can be done via SCITT through SW development lifecycle)
* DSCA signing SCITT interaction – existing services that sign artifacts. Need to capture interaction with SCITT – Sigstore, Notary V2, Maven ecosystem, GPG
