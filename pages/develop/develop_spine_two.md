---
title: Spine 2
keywords: development
tags: [development]
sidebar: overview_sidebar
permalink: develop_spine_two.html
summary: An overview of the interface mechanisms available as part of Spine 2.
---

## Spine 2 Interfaces ##

Overview of Spine 2 operation.

### Simpler Synchronous Web Services ###

- FHIR APIs
- Proprietary APIs

#### Spine Security Proxy ####

The MESH service provides a much improved asynchronous channel for any kind of messages or file transfers across the NHS. It is designed with great elasticity but has a delivery time measured in minutes<sup>1</sup> which will not be suitable for all messaging scenarios. For situations in which a human user is waiting for a response to a query or transaction the Spine Security Proxy (SSP) has been introduced. The SSP provides a lightweight mediator for communications between to NHS Organisations. It is currently developed and awaiting live implementation.
The SSP avoids the need for endpoints to open their firewalls to potentially hundreds of other unknown organisations in the NHS and instead allows them just to open a firewall to the Spine.
The SSP will be connected to the planned Spine Internet Gateway. This will provide access to API providers for internet facing consuming removing the need for each API provider to implement and manage their own internet gateways;
The SSP removes the need for a burdensome PKI infrastructure by allowing endpoints to simply trust the spine certificates for communication, using the existing security mechanisms. It also performs system authorisation ensuring the calling system is allowed to retrieve messages to the type defined in their registration. It will provide an additional level of protection from threats and introduces ability to lock out malicious endpoints from all other NHS endpoints simultaneously at the mediating layer. It provides a platform for implementing more sophisticated authentication and authorisation methods once rather than requiring all systems across the NHS to implement these e.g. Citizen Identity and specifically for Patient Facing Services or Consent management controls.
The SSP will provide a single point for the collection and analysis of data movement across the NHS in real time. For example it will allow the NHS to understand how GP data is used across care settings to improve service redesign. The SSP will enable tracking of performance across the system in real time, flagging performance issue immediately and implementing throttling to protect API providers.
The SSP will be wrapped in service levels for both consumer and API providers. 1st line support can be provided by the NHS Digital service management team reducing the burden on suppliers because many issues will be resolved without having to involve the API provider e.g. certificate issues, malformed messages etc. It will enable improved defect analysis and fault resolution will benefit providing an unbiased central point to identify where a problem resides via clear logging and diagnostic information.
Finally a centrally managed and funded accreditation process is being created to support the deployment of the SSP and the APIs provided.  This will involve a single pairing between an API provider and the SSP allowing subsequent consumers to pair once with the SSP and have access to all suppliers who implement the APIs they have been accredited against.
The first programme to utilise the SSP is the GP Connect Programme. This programme plans to open up primary care data by exposing standardised FHIR APIs for accessing GP Practice data. This is expected to be the first of many programmes to take advantage of the SSP.

<sup>1</sup>Typically up to 20 mins including poll time. Although these times are likely to be improved as we refine the system.

### Forward messaging ###

#### MESH ####

The previous version of the spine supported the forwarding of messages between NHS systems using two ebXML forwarding patterns. However, the cost and complexity of implementing these proved so onerous that they were never voluntarily used by NHS organisations and suppliers<sup>2</sup>.
So the Digital Delivery Centre<sup>3</sup> (DDC) was already aware of the need for an alternative effective asynchronous messaging solution. As part of the renewal of the Data Transfer Service the DDC recognised that DTS had been popular as a transport.

This was a result of a variety of factors:

1. It was free;
2. It was easy to implement, relying only the installation of a client and the ability to interact with operating system directories;
3. It was resilient, allowing senders to send while recipient systems were offline.


Spine2 thus decided that the ‘store and poll’ pattern implemented by DTS would provide a favourable overall national solution for asynchronous messaging communications. The new Message Exchange for Social care and Health (MESH) builds upon the DTS service. It maintains all the benefits of DTS but also introduces better performance, higher scalability (to support ever greater numbers of messages) and multiple comms channels.
Organisations interact with MESH by uploading files for other recipients to the recipient’s virtual inbox and by polling their own virtual inbox for messages intended for them. Private suppliers typically support a MESH endpoint, integrating their systems with it on behalf of their NHS customer organisations. But NHS Organisations are equally able to apply for MESH endpoints directly.

<sup>2</sup>They were only ever used at great expense by the e-RS and GP2GP programmes.
<sup>3</sup>The DDC is the department of NHS Digital which builds the Spine and a number of other national services.

##### Multi-channel MESH #####

Organisations can interact with the MESH by using any one of:

1.	A free MESH downloadable client, available in Java or Perl. This is most suitable for previous DTS endpoints and endpoints of medium technical capability.
2.	Direct interaction with the MESH API. This is most suitable for endpoints that want greater control over the pushing and the polling of their data;
3.	A MESH GUI. This is an online application for accessing and uploading MESH messages. Users log onto the MESH GUI using two factor authentication either with an NHS smart card or alternative authentication mechanism. Once logged in they can see the messages intended for their mailbox and upload and address messages to other endpoints.

