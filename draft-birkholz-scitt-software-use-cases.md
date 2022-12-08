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

This document includes a collection of representative Software Supply Chain Use Case Descriptions. These use cases aim at identifying software supply chain problems that the industry faces today and acts as a guideline for developing a comprehensive solution for these class of scnenarios.

--- middle

# Introduction {#intro}

Modern software applications are an intricate mix of first-party and third-party code, development practices and tools, deployment methods and infrastructure, and interfaces and protocols. The software supply chain comprises all elements associated with an application's design, development, build, integration, deployment, and maintenance throughout its entire lifecycle. The complexity of software coupled with a lack of lifecycle visibility increases the risks associated with system attack surface and the number of cyber threats capable of harmful impacts, such as exfiltration of data, disruption of operations, and loss of reputation, intellectual property, and financial assets. There is a need for a platform architecture that will allow consumers to know that suppliers maintained appropriate security practices without requiring access to proprietary intellectual property. SCITT-enabled products and analytics solutions will assist in managing compliance and assessing risk to help prevent and detect supply chain attacks across the entire software lifecycle while prioritizing data privacy.

## Terminology {#terms}

{::boilerplate bcp14-tagged}

# Generic Problem Statement

Supply chain security is a paramount prerequisite to successfully protect not only consumers that use supply chain outputs, e.g., products used in critical infrastructure, aerospace, but also to protect the economy, public health, and safety as a whole. Supply chain security has historically focused on risk management practices to safeguard logistics, meet compliance regulations, demand forecasts, and optimize inventory. While these elements are foundational to a healthy supply chain, an integrated cyber security-based perspective of the software supply chains remains broadly undefined. Recently, the global community has experienced numerous supply chain attacks targeting weaknesses in software supply chains. As illustrated in {{lifecycle-threats}}, a software supply chain attack may leverage one or more lifecycle stages and directly or indirectly target the component.

<!-- ![SCITT_SW_Use_Case](https://user-images.githubusercontent.com/100775190/197196387-f8f835ba-7023-4223-98c9-3d8ec197e658.svg) -->
~~~~
generic supply chain threats diagram here
~~~~
{: #lifecycle-threats title="Example Lifecycle Threats"}

DevSecOps often depends on third-party and open-source solutions. These dependencies can be quite complex throughout the supply chain and render the checking of lifecycle compliance difficult. There is a need for manageable auditability and accountability of digital products. Typically, the range of types of statements about digital products (and their dependencies) is vast, heterogeneous, and can differ between community policy requirements. Taking the type and structure of all statements about digital and products into account might not be possible. Examples of statements may include commit signatures, build environment and parameters, software bill of materials, static and dynamic application security testing results, fuzz testing results, release approvals, deployment records, vulnerability scan results, and patch logs. In consequence, instead of trying to understand and describe the detailed syntax and semantics of every type of statements about digital products, the SCITT architecture focusses on ensuring statement authenticity, visibility/transparency, and intends to provide scalable accessability. The following use case illustrate the scope of SCITT and elaborate on the generic problem statement above.

# Notational Implementation

TBD

~~~~
deployment chain diagram here
~~~~
{: #deployment-chain title="Deployment Example of SCITT in Software Development"}

# Software Supply Chain Use Cases

## Updated Statements over Time

A released software product is accompanied by a set of complementary statements about it's security compliance and is deemed secure by both producers and consumers.
After some time, new statements produced and published by 3rd parties show that a software component used in the software product contains potentially weakness.
Over time, a statement of another 3rd party illustrates that the weakness is exposed in the software product in a way that it is an exploitable vulnerability.
The producer of the software product now provides a statement that confirms the linking of software component vulnerability with the software product and also issues an advisory statement how to mitigate the vulnerability ad-hoc.
Later, the producer provides an updated software product that still uses the vulnerable software component, but shields the issue in a fashion that inhibits exploitation.
A second update of the software product includes a patch to the affected software component created by the software product producer itself.
A third update then includes an updated version of the formerly insecure software component - both the software product and the affected software component are deemed secure by both producer and consumers in this release.

A consumer wants:
* to know where to get these statements from producers and 3rd parties related to the software product in a timely and unambiguous fashion,
* how to attribute them to an authoritative issuer,
* how to associate the statements in a meaningful manner, and
* how to consistently, efficiently, and homogeneously check their authenticity.

There is no standardized way to:
* know the various sources of statements,
* how to express the provenance and historicity of statements,
* how to related/link various heterogeneous statements in a simple fashion,
* check that the statement actually is coming from a source that actually has the authority to issue that statement

## Authenticity of Promoted Software Products

A software component source (e.g., a library) released by a certain original producer is becoming popular.
The released software component source is accompanied by a statement of authenticity (e.g., a detached signature).
Over time, there is an increasing amount of providers of the same version of the software component source over the Internet.
Some popular providers package the software component and provide the package with a proof of authenticity using their own issuer authority.
Some of these packages include the original statement of authenticity, some do not.
After some time, some providers do not offer the exact same software component source, but pre-compiled software component binaries.
Some sources do not provide the exact same software component, but include patches and fixes produced faster by 3rd parties than the original producer.
In the end, there is vast number of forms the original software component source is distributed and promoted by.

A consumer wants:
* to understand, if a certain provider is actually the original provider or a promoter,
* to know, if and how the source (or resulting binary) of a promoted software component is different to the original software component,
* to check the provenance and history of a software component's source back to its origin, and
* to assess whether to trust a promoter of not.

There is no standardized way to:
* to reliably discern a provider that is the original producer from a provider that is a trustworthy promoter or from an illegitimate provider,
* track the provenance path from an original producer to a certain provider
* to check for the trustworthiness of a provider
* to check the integrity of modifications or transformations done by a provider

## Firmware Delivery to large set of constrained IoT Devices

### Introduction

Firmware is ubiquitous. It is in phone, watch, TV, alarm clock, baby monitor, WiFi devices and possibly even in light bulbs if one uses LED lamps. In any given desktop or Personal Computer (PC) there is a BIOS or UEFI type firmware that people are familiar with, but there are also scores of other hidden firmware blobs running on small controllers which power things like management engines, keyboards, network cards, hard disks, SSD's etc.

Firmware is powerful, it runs in a highest privilege level possible and is often the bedrock on which the security story of the devices it powers.


### Personal Health Monitoring Systems

Personal health monitoring devices, i.e., eHealth devices are typically battery driven and located physically on or under user control to monitor some bodily function, such as temperature, blood pressure or pulse rate. These devices typically connect to the Internet through an intermediary base station, using wireless technologies. This connection is used to report the monitored data and also to update the firmware on the health monitoring system. This public network and open distribution system produces its own security challenges.

Today, the best-in-class firmware vendors who supply the firmware also provide an update framework, which verifies the integrity and authenticity of firmware updates before allowing them to be installed.

#### Firmware Delivery Problem Summary

Even with a robust firmware update system the following problems remain as given below:

* How does the client applying the firmware update on the system know, that the received firmware is not faulty or even malicious ?

* What if the signing identity used to assert the authenticity of the firmware is somehow used to sign unintended updates ?

* How can one ascertain that the released firmware is not subverted or compromised due to an insider risk - be it malicious or otherwise ?

* How the publisher themselves even know that there deliverable has been compromised in some way, can they trust their  key protection or audit logging ?

* How  the update client on an instance of health monitoring system know that they have been given the same update as all other devices or one especially crafted for just a small subset of fleet of devices ?

## Software Integrator assembling a software product for a smart car
### Introduction

Software Integration is a complex activity. It essentially implies combining various different software components coming from a range of suppliers and producing a combined executable to be given to a Device Manufacturer. Then the executable is loaded into the device, as part of device assembly.

The complexity adds a level of security vulnerability into the delivered software.

### Assembly of a Components in a Smart Car

SoftAuto Ltd and Smart Cars Ltd are two different companies that source developed integrated software that can be loaded into autonomous vehicles they produce. Both these companies, source integrated software solution from Micro Coding Wizard (MCW) a fictitious company that sells integrated software solutions that can be loaded into specific vehicle product. MCW assembles the OS from Vendor OS-X that is built on top of Firmware released by Component Vendor-A and then integrates a package manager and some open source libraries to make the final software product. The assembled software is loaded onto a car manufactured by Smart Cars Ltd. The car is been sold and is been actively used by Customer-Y.

### Software Problem Summary

* While the software is been running on the automated vehicle, a periodic vulnerability scanning software detects some known security issue with one of the component. Customer-Y is prompted with a "Warning Indicator" on the dashboard. As a result, Customer-Y reports the problem to Smart Cars Ltd.

* Smart Cars Ltd, while not very sure what could be the problem, under panic communicates to MCW and requests them to look into the problem.

* MCW does initial investigation and suspects that the binary received from Vendor OS-X has some problems. It demands specific environment and architectural details associated with the built operating systems binary to ascertain that the software was produced without any tampering by the Vendor OS-X.

* Unfortunately there is no way for the integrator to know, if the binary was compromised, so the integrator is concerned they may have delivered malware unknowingly to their customers.

* Vendor OS-X attempts to show that it did all the steps correctly. It does disclose information about the binary they delivered. In addition to this, they also demonstrated the build environment and the architecture, they used during the build.

* However there is no "Verifiable Proofs" of the statement made by Vendor OS-X.

* MCW, Smart Cars Ltd., and Customer-Y now has to trust without any means of verifying the claims made by Vendor OS-X.

* Vendor OS-X thinks there is some mistake on the part of MCW that has led to this situation.

* The deadlock continues, with no clear resolution.

* This eventually leads to loss of reputation and company closure for Vendor OS-X.


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
