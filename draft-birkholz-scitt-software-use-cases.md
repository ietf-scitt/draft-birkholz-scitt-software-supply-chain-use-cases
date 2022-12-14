---
v: 3

title: Detailed Software Supply Chain Uses Cases for SCITT
abbrev: SCITT SW Supply Chain
docname: draft-birkholz-scitt-software-use-cases-latest
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
  - ins: Y. Deshpande
    name: Yogesh Deshpande
    org: ARM
    email: yogesh.deshpande@arm.com
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

normative:

informative:

--- abstract

This document includes a collection of representative Software Supply Chain Use Case Descriptions. These use cases aim to identify software supply chain problems that the industry faces today and acts as a guideline for developing a comprehensive solution for these classes of scenarios.

--- middle

# Introduction {#intro}

Modern software applications are an intricate mix of first-party and third-party code, development practices and tools, deployment methods and infrastructure, and interfaces and protocols. The software supply chain comprises all elements associated with an application's design, development, build, integration, deployment, and maintenance throughout its entire lifecycle. The complexity of software coupled with a lack of lifecycle visibility increases the risks associated with system attack surface and the number of cyber threats capable of harmful impacts, such as exfiltration of data, disruption of operations, and loss of reputation, intellectual property, and financial assets. There is a need for a platform architecture that will allow consumers to know that suppliers maintained appropriate security practices without requiring access to proprietary intellectual property. SCITT-enabled products and analytics solutions will assist in managing compliance and assessing risk to help prevent and detect supply chain attacks across the entire software lifecycle while prioritizing data privacy.

## Terminology {#terms}

{::boilerplate bcp14-tagged}

# Generic Problem Statement

Supply chain security is a paramount prerequisite to successfully protect consumers and minimize economic, public health, and safety impacts. Supply chain security has historically focused on risk management practices to safeguard logistics, meet compliance regulations, demand forecasts, and optimize inventory. While these elements are foundational to a healthy supply chain, an integrated cyber security-based perspective of the software supply chains remains broadly undefined. Recently, the global community has experienced numerous supply chain attacks targeting weaknesses in software supply chains. As illustrated in {{lifecycle-threats}}, a software supply chain attack may leverage one or more lifecycle stages and directly or indirectly target the component.

<!-- ![SCITT_SW_Use_Case](https://user-images.githubusercontent.com/100775190/197196387-f8f835ba-7023-4223-98c9-3d8ec197e658.svg) -->
~~~~
generic supply chain threats diagram here
~~~~
{: #lifecycle-threats title="Example Lifecycle Threats"}

DevSecOps often depends on third-party and open-source solutions. These dependencies can be quite complex throughout the supply chain and render the checking of lifecycle compliance difficult. There is a need for manageable auditability and accountability of digital products. Typically, the range of types of statements about digital products (and their dependencies) is vast, heterogeneous, and can differ between community policy requirements. Taking the type and structure of all statements about digital and products into account might not be possible. Examples of statements may include commit signatures, build environment and parameters, software bill of materials, static and dynamic application security testing results, fuzz testing results, release approvals, deployment records, vulnerability scan results, and patch logs. In consequence, instead of trying to understand and describe the detailed syntax and semantics of every type of statement about digital products, the SCITT architecture focuses on ensuring statement authenticity, visibility/transparency, and intends to provide scalable accessibility. The following use case illustrates the scope of SCITT and elaborate on the generic problem statement above.

<!--
# Notational Implementation

TBD

~~~~
deployment chain diagram here
~~~~
{: #deployment-chain title="Deployment Example of SCITT in Software Development"}
-->

# Software Supply Chain Use Cases

## Trust Bond between Package Supplier and the Signing Authority

A certain software component product is created and packaged by a Supplier.
The package by itself does not include a proof of authenticity.
A signing authority is tasked with adding a proof of authenticity.
Trust has to be established from the Supplier towards the Signing Authority - and vice versa.
The mutual trust relationship (trust bond) between Supplier and Signing Authority is established per each individual software component package.

A consumer of a released software wants:

* to understand and verify that an actual trust bond exists between the Supplier of a certain software component package and the Signing Authority of that software component package.

There is no standardized way to:

* enable the consumer to verify that a trust bond for a certain software component package exists and is still valid.

## Scalable Determination of Trustworthiness in Multi-Stakeholder Ecosystems

Authoritative entities, such as auditing or code-review companies, certification entities or government bodies, continuously produce statements about software products and identifiable software components.
Such statements can vouch for the trustworthiness of a software product or the lack thereof.
Consumers of these statements include entities, such as distributing entities, as well as end users.
There can be one or more entities that produce statements relevant to one or more of these consumer groups.
Discovery of all sources of statements and/or the identity of authoritative entities creates significant cost not all consumer groups can afford.
Some authoritative entities actively do not acknowledge other authoritative entities that highlight a lack of trustworthiness of certain released software products.
In the end, identifying all relevant statements from multiple sources typically ends up to be a responsibility of the consumer.

A consumer of released software wants:
* to offload the burden of identifying all relevant authoritative entities to an entity who does this on their behalf
* to offload the burden to filter from and select all statements that are applicable to the released software product to an entity who does this on their behalf
* to make informed decisions on which authoritative entities to believe based on the best visibility of all authoritative entities possible

There is no standardized way to:
* aggregate large numbers of related statements in one place and discover them there
* referencing other statements via a statement
* identifing or discover all (or at least a critical mass) of relevant authoritative entities

## Updated Statements over Time

A released software product is accompanied by a set of complementary statements about it's security compliance and is deemed trustworthy by both producers and consumers.
After some time, new statements produced and published by third-parties show that a software component used in the software product contains a potential weakness.
Over time, a statement from another third-party illustrates that the weakness is exposed in the software product in a way that it is an exploitable vulnerability.
The producer of the software product now provides a statement that confirms the linking of software component vulnerability with the software product and also issues an advisory statement on how to mitigate the vulnerability ad-hoc.
Later, the producer provides an updated software product that still uses the vulnerable software component but shields the issue in a fashion that inhibits exploitation.
A second update of the software product includes a patch to the affected software component created by the software product producer.
A third update includes an updated version of the formerly insecure software component. For this release, both the software product and the affected software component are deemed secure by the producer and consumers.

A consumer of a released software wants:

* to know where to get these statements from producers and third-parties related to the software product in a timely and unambiguous fashion,
* how to attribute them to an authoritative issuer,
* how to associate the statements in a meaningful manner via a set of well-known semantic relationships, and
* how to consistently, efficiently, and homogeneously check their authenticity.

There is no standardized way to:

* know the various sources of statements,
* how to express the provenance and historicity of statements,
* how to related/link various heterogeneous statements in a simple fashion, and
* check that the statement comes from a source with authority to issue that statement.

## Authenticity of Promoted Software Products

A software component source (e.g., a library) released by a certain original producer is becoming popular.
The released software component source is accompanied by a statement of authenticity (e.g., a detached signature).
Over time, there has been an increasing amount of providers of the same version of the software component source over the Internet.
Some popular providers package the software component and provide the package with proof of authenticity using their own issuer authority.
Some packages include the original statement of authenticity, and some do not.
Over time, some providers no longer offer the exact same software component source but pre-compiled software component binaries.
Some sources do not provide the exact same software component but include patches and fixes produced by third-parties, as these emerge faster than solutions from the original producer.
Due to complex distribution and promotion lifecycle scenarios, the original software component takes myriad forms.

A consumer of a released software wants:

* to understand if a particular provider is actually the original provider or a promoter,
* to know if and how the source, or resulting binary, of a promoted software component differs from the original software component,
* to check the provenance and history of a software component's source back to its origin, and
* to assess whether to trust a promoter or not.

There is no standardized way to:

* to reliably discern a provider that is the original producer from a provider that is a trustworthy promoter or from an illegitimate provider,
* track the provenance path from an original producer to a particular provider
* to check for the trustworthiness of a provider
* to check the integrity of modifications or transformations done by a provider

## Checking the History of Statements about Software by Auditors

An organization has established procurement requirements and compliance policies for software use.
In order to allow the acquisition and deployment of software in certain security domains of the organization, a check of software quality and characteristics must succeed.
Compliance and requirement checking includes audits of the results of organisational procedures and technical procedures, which can originate from checks conducted by the organization itself or checks conducted by trusted third parties.
Consecutively, consumers of statements about a released software can be auditors.
Examples of procedure results important to audits include: available fresh and applicable code reviews, certification documents (e.g., FIPS or Common Criteria), virus scans, vulnerability disclosure reports (fixed or not fixed), security impact or applicability justification statements.
Relevant compliance, requirement, and check result documents originate from various sources and include a wide range of representations and formats.

A consumer of a released software wants:

* to provide methods with different levels of complexity to auditors of a released software
* expects the creator or distributor of released software to enable audit procedures and make corresponding documents visible and available
* the cost of audits to be manageable and scale well
* complete visibility and accessibility to documents required for audits

There is no standardized way to:

* discover and associate relevant documents and check results required for various types of audits
* assert the authenticity and provenance of documents relevant to audits in a deterministic and uniform fashion
* check the validity of identity statements about relevant documents after the fact (when they were made) in a consistent, long-term fashion
* allow for more than one level of complexity of audit procedures (potentially depending on criticality)

## Checking the Authenticity of Software Components in Isolated or Air-Gapped Infrastructure

Some software is deployed on systems not connected to the Internet.
Authenticity checks for off-line systems can occur at time of deployment of released software.
Off-line systems require appropriate configuration and maintenance to be able to conduct useful authenticity checks.
If the off-line systems are operation are part of constrained node environments, they do not possess the capabilities to process and evaluate all kinds of different authenticity proofs that come with a released software.

A consumer of a released software wants:

* a proof of authenticity that can be checked by an off-line system for vast periods of time after system deployment
* a proof of authenticity to be small and as uniform as possible to allow for application in constrained node environments
* a simple and low cost way to update the configuration of a system component in charge of validity or authenticity cecking

There is no standardized way to:

* provide an authenticity proof that can be checked by off-line systems in a simple and uniform fashion
* enable rich systems, regular systems, and constrained systems to conduct authenticity checks via the same procedure / code base
* manage trust relationships with respect to the producers of authenticity statements in a fashion that scales from application such as global open source repositories down to off-line constrained devices

## Firmware Delivery to large set of constrained IoT Devices

### Introduction

Firmware is ubiquitous in IoT devices (e.g., appliances, televisions, smart LED bulbs, HVAC, automobiles), runs at the highest privilege level possible, and is often the bedrock on which the security story of the devices it powers.

Firmware is powerful. It runs in the highest privilege level possible and is often the bedrock on which the security story of the devices it powers.


### Personal Health Monitoring Systems

Personal health monitoring devices, i.e., eHealth devices, are generally battery driven and offer health telemetry monitoring, such as temperature, blood pressure, and pulse rate. These devices typically connect to the Internet through an intermediary base station using wireless technologies. Through this connection, the telemetry data and analytics transfer, and devices receive firmware updates when published by the vendor. The public network, open distribution system, and firmware update process create several security challenges.

Today, the best-in-class firmware vendors who supply the firmware also provide an update framework, which verifies the integrity and authenticity of firmware updates before allowing installation.

#### Firmware Delivery Problem Summary

Even with a robust firmware update system, the following problems remain as given below:

* How does the client applying the firmware update on the system know that the received firmware is not faulty or malicious?

* What if the signing identity used to assert the authenticity of the firmware is somehow used to sign unintended updates?

* How can one ascertain that the released firmware is not subverted or compromised due to an insider risk - be it malicious or otherwise?

* How does the publisher even know that their deliverable has been compromised? Can they trust their key protection or audit logging?

* How does the update client on an instance of a health monitoring system know that they have been given the same update as all other devices or one specially crafted for just a small subset of a fleet of devices?

## Software Integrator assembling a software product for a smart car
### Introduction

Software Integration is a complex activity. It implies combining various software components from multiple suppliers and producing an integrated package deployed as part of device assembly and provisioning.

Integration complexity creates a higher risk of security vulnerabilities to the delivered software.

### Assembly of Components in a Smart Car

SoftAuto Ltd and Smart Cars Ltd are two different companies that source third-party integrated software for the autonomous vehicles they produce. Both these companies source integrated software solutions from Micro Coding Wizard (MCW), a fictitious company that sells integrated software solutions. MCW assembles the OS from Vendor OS-X that is built on top of firmware released by Component Vendor-A and then integrates a package manager and some open-source libraries to make the final software product. The assembled software is loaded onto a car manufactured by Smart Cars Ltd. The car has been sold and is actively used by Customer-Y.

### Software Problem Summary

* While the software runs on the automated vehicle, periodic vulnerability scanning software detects a known security issue with one component. Customer-Y is prompted with a "Warning Indicator" on the dashboard. As a result, Customer-Y reports the problem to Smart Cars Ltd.

* Smart Cars Ltd, has little insight into the root cause of the error, communicates to MCW, and requests them to look into the problem.

* MCW does an initial investigation and suspects that the binary received from Vendor OS-X has some problems. It demands specific environment and architectural details associated with the built operating systems binary to ascertain that the software was produced without tampering by Vendor OS-X.

* Unfortunately, there is no way for the integrator to know if the binary was compromised, so the integrator is concerned they may have delivered malware unknowingly to their customers.

* Vendor OS-X attempts to show that it did all the steps correctly. It does disclose information about the binary they delivered. In addition, they also reveal their build environment and the architecture they used during the build.

* However, there are no "Verifiable Proofs" of the statement made by Vendor OS-X.

* MCW, Smart Cars Ltd., and Customer-Y now have to trust without the ability to verify the claims made by Vendor OS-X.

* Vendor OS-X thinks there is some mistake on the part of MCW that has led to this situation.

* The deadlock continues, with no clear resolution.

* This eventually leads to a loss of reputation and company closure for Vendor OS-X.

# Summary of Problem Statements
* Consumers want to understand and verify that an actual trust bond exists between the Supplier of a certain software component package and the Signing Authority of that software component package (4.1.1)
* Consumers want to obtain statements from producers and third-parties related to the software product in a timely and unambiguous fashion (4.2.1)
* Consumers want to attribute statements to an authoritative issuer (4.2.2)
* Consumers want to associate statements with other statements in a meaningful manner (4.2.3)
* Consumers want to consistently, efficiently, and homogeneously check the authenticity of statements (4.2.4)
* Consumers want to understand if a particular provider is actually the original provider or a promoter (4.3.1)
* Consumers want to know if and how the source, or resulting binary, of a promoted software component differs from the original software component (4.3.2)
* Consumers want to check the provenance and history of a software component's source back to its origin (4.3.3)
* Consumers want to assess whether to trust a promoter or not (4.3.4)
* To be continued...
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
