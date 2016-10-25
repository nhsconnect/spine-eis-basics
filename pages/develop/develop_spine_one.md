---
title: Spine 1
keywords: development
tags: [development]
sidebar: overview_sidebar
permalink: develop_spine_one.html
summary: An overview of the interface mechanisms available as part of Spine 1.
---

## Spine 1 Interfaces ##

Spine1 supported a number of synchronous and asynchronous transport formats both for accessing Spine data and for forwarding data via the Spine to other parties. Chapter 3 of the EIS, the “Message Interaction Map<sup>1</sup>” describes which messages use which possible Spine1 formats.

### ebXML ###

Spine1 provided ebXML interfaces for asynchronous communications. This messaging format requires consumer parties to expose a server compliant with ebXML MSH standards as well as applying the additional requirements defined in EIS part 2.
ebXML Asynchronous communications are used for all update messages on the spine as well as a number of larger queries such as the Advanced Traces to the demographics services (aka. PDS).
The payload for majority of ebXML communications are HL7v3 messages defined in the Message Implementation Manual (MIM). Spine2 supports messages from a number of different historic versions of the MIM.

In the future Spine is not expecting to provide any asynchronous messaging interfaces for accessing Spine services as the high performance of Spine2 negates the need for such more elastic transport protocols.

<sup>1</sup>See for example document “2087 EIS11.8--Part 3--MessageInteractionMap.doc”

### Web Services ###

Spine also provided a variety of information via synchronous web service interfaces. These interfaces use a SOAP envelope with a WS-Addressing header to define meta-data about the messages.
The payload for web service interfaces is either an HL7v3 message or a proprietary XML message. For HL7 messages the payload will again be defined in the Message Implementation Manual.
For proprietary message payloads the format will always be defined an a specialised chapter of the EIS. Such payloads may then also carry an additional HL7v3 wrapper in order to carry some of the author and organisation data required by the Spine1 systems. Such messages are referred to as pseudo HL7 Web Services.

### Forward messaging ###

The Spine supports two legacy forward messaging protocols, both ebXML based. Forward Reliable (aka. Multi-hop intermediary reliability) is used for GP2GP messages and Forward Express (aka. Multi-hop intermediary reliability) is used for e-RS messaging. Note that both formats are equally reliable. Both patterns use the ebXML features described in Part 2 of the EIS (“2087 EIS12.2--Part 2--MHS.doc”). However, users should also review the patterns description in the document “2086 MHS Behaviour Patterns 9.5.doc”.

