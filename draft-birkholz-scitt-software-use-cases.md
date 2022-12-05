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

DevSecOps relies on third-party and open-source solutions. An unfortunate effect that also results from this dependency is an increase of supply chain complexity and a corresponding reduction of the visibility of w.r.t. lifecycle compliance. One solution approach to counter that effect is to enhance the auditability and accountability of digital products by using an interoperable, scalable, and flexible decentralized architecture including a transparent registry bolstering visibility and . The required software artifacts are highly variable based on community policy requirements, and the solution approach should be artifact agnostic to enable adaptation to these broad policies. Example artifacts may include commit signatures, build environment and parameters, software bill of materials, static and dynamic application security testing results, fuzz testing results, release approvals, deployment records, vulnerability scan results, and patch logs.

# Notational Implementation

TBD

~~~~
deployment chain diagram here
~~~~
{: #deployment-chain title="Deployment Example of SCITT in Software Development"}

# Software Supply Chain Use Cases

## Firmware Delivery to large set of constrained IoT Devices

### Introduction

Firmware is ubiquitous. It is in phone, watch, TV, alarm clock, baby monitor, WiFi devices and possibly even in light bulbs if one uses LED lamps. In any given desktop or Personal Computer (PC) there is a BIOS or UEFI type firmware that people are familiar with, but there are also scores of other hidden firmware blobs running on small controllers which power things like managment engines, keyboards, network cards, hard disks, SSD's etc.

Firmware is powerful, it runs in a highest previlege level possible and is often the bedrock on which the security story of the devices it powers.


### Personal Health Monitoring Systems

Personal health monitoring devices, i.e., eHealth devices are typically battery driven and located physically on or under user control to monitor some bodily function, such as temperatire, blood pressure or pulse rate. These devices typically connect to the Internet through an intermediary base statation, using wireless technologies. This connection is used to report the monitored data and also to update the firmware on the health monitoring system. This public network and open distribution system produces its own security challenges.

Today, the best-in-class firmware vendors who supply the firmware also provide an update framework, which verifies the integrity and authenticity of firmware updates before allowing them to be installed.

#### Firmware Delivery Problem Summary

Even with a robust firmware update system the following problems remain as given below:

* How does the client applying the firmware update on the system know, that the received firmware is not faulty or even malicious ?

* What if the signing identity used to assert the authenticity of the firmware is somehow used to sign unintended updates (whether through outright compromise as in the Realtek identity used to sign the Stuxnet worm)?

* How can one ascertain that the released firmare is not subverted or compromised due to an insider risk - be it malicious or otherwise ?

* How the publisher themselves even know that there deliverable has been compromised in some way, can they trust their  key protection or audit logging ?

* How  the update client on an instance of health monitoring system know that they have been given the same update as all other devices or one especially crafted for just a small subset of fleet of devices ?

## Software Integrator assembling a software product for a smart car
### Introduction

Software Integration is a complex activity. It essentially implies combining various different software components coming from a a range of suppliers and producing a combined executable to be given to a Device Manufacturer. Then the executable is loaded into the device, as part of device assembly.

The complexity adds a level of security vulnerability into the delivered software.

### Assembly of a Components in a Smart Car

SoftAuto Ltd and Smart Cars Ltd are two different companies that source developed integrated software that can be loaded into autonmous vehicles they produce. Both these companies, source integrated software solution from Micro Coding Wizard (MCW) a fictitious company that sells integrated software solutions that can be loaded into specific vehicle product. MCW assembles the OS from Vendor OS-X that is built on top of Firmware released by Component Vendor-A and then integrates a package manager and some open source libraries to make the final software product. The assembled software is loaded onto a car manufactured by Smart Cars Ltd. The car is been sold and is been actively used by Customer-Y.

### Software Problem Summary

* While the software is been running on the automated vehicle, a periodic vulnerability scanning software detects some known security issue with one of the component. Customer-Y is prompted with a "Warning Indictor" on the dashboard. As a result, Customer-Y reports the problem to Smart Cars Ltd.

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
