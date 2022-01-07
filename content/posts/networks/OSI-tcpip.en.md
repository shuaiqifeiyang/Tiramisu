---
title: "OSI model and TCP/IP model"
date: 2020-01-07T09:58:03-08:00
draft: false
tags: ["Networks"]
categories: ["Networks"]
---
<!--more-->

## OSI Model

7 Layers of OSI Model:

|   | Layer        | Function                                                                                                                                                                                                                                                                               |
| - | ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | Physical     | Transmission and reception of raw bit streams over a physical medium                                                                                                                                                                                                                   |
| 2 | Data link    | Reliable transmission of data frames between two nodes connected by a physical layer                                                                                                                                                                                                   |
| 3 | Networking   | Structuring and managing a multi-node network, including[addressing](https://en.wikipedia.org/wiki/Address_space), [routing](https://en.wikipedia.org/wiki/Routing) and [traffic control](https://en.wikipedia.org/wiki/Network_traffic_control)                                                |
| 4 | Transport    | Reliable transmission of data segments between points on a network, including[segmentation](https://en.wikipedia.org/wiki/Packet_segmentation), [acknowledgement](https://en.wikipedia.org/wiki/Acknowledgement_(data_networks)) and [multiplexing](https://en.wikipedia.org/wiki/Multiplexing) |
| 5 | Session      | Managing communication[sessions](https://en.wikipedia.org/wiki/Session_(computer_science)), i.e., continuous exchange of information in the form of multiple back-and-forth transmissions between two nodes                                                                               |
| 6 | Presentation | Translation of data between a networking service and an application; including[character encoding](https://en.wikipedia.org/wiki/Character_encoding), [data compression](https://en.wikipedia.org/wiki/Data_compression) and [encryption/decryption](https://en.wikipedia.org/wiki/Encryption)  |
| 7 | Application  | High-level[APIs](https://en.wikipedia.org/wiki/API), including resource sharing, remote file access                                                                                                                                                                                       |

* Physical layer, data link layer and network layer are called *media layers*, transport layer, session layer, presentation layer and application layer are called *host layers*.

## TCP/IP Model

- The Internet [application layer](https://en.wikipedia.org/wiki/Application_layer) maps to the OSI application layer, presentation layer, and most of the session layer.
- The TCP/IP [transport layer](https://en.wikipedia.org/wiki/Transport_layer) maps to the graceful close function of the OSI session layer as well as the OSI transport layer.
- The [internet layer](https://en.wikipedia.org/wiki/Internet_layer) performs functions as those in a subset of the OSI network layer.
- The [link layer](https://en.wikipedia.org/wiki/Link_layer) corresponds to the OSI data link layer and may include similar functions as the physical layer, as well as some protocols of the OSI's network layer.
