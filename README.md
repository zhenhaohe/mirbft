# MirBFT Library

This open-source project is part of [Hyperledger Labs](https://labs.hyperledger.org/labs/mir-bft.html).

It aims at developing a production-quality implementation of:
- a general framework for easily implementing distributed protocols
- the ISS Byzantine fault tolerant consensus protocol.

ISS is the new generation of the [Mir-BFT protocol](https://arxiv.org/abs/1906.05552)
and a link to its detailed description will be added here shortly.
The aim of the Mir-BFT library is integration with Hyperledger Fabric, specifically its ordering service.
Being framed as a library, however, MirBFT's goal is also to serve as a general-purpose high-performance BFT component
of other projects as well.

The [research branch](https://github.com/hyperledger-labs/mirbft/tree/research) contains code developed independently
as a research prototype and was used to produce experimental results
for the [research paper](https://arxiv.org/abs/1906.05552).

## Current status

This library is in development and not usable yet.
This document describes what the library _should become_ rather than what it _currently is_.
This document itself is more than likely to still change.
You are more than welcome to contribute to accelerating the development of the MirBFT library.
Have a look at the [Contributions section](#contributing) if you want to help out!

[![Build Status](https://github.com/hyperledger-labs/mirbft/actions/workflows/test.yml/badge.svg)](https://github.com/hyperledger-labs/mirbft/actions)
[![GoDoc](https://godoc.org/github.com/hyperledger-labs/mirbft?status.svg)](https://godoc.org/github.com/hyperledger-labs/mirbft)

## Overview

MirBFT is a library implementing the ISS protocol (and, in the future, other protocols)
in a network transport, storage, and cryptographic algorithm agnostic way.
MirBFT hopes to be a building block of a next generation of distributed systems,
providing an implementation of [atomic broadcast](https://en.wikipedia.org/wiki/Atomic_broadcast)
which can be utilized by any distributed system.

MirBFT/ISS improves on traditional atomic broadcast protocols
like [PBFT](https://www.microsoft.com/en-us/research/wp-content/uploads/2017/01/p398-castro-bft-tocs.pdf) and Raft
which always have a single active leader by allowing concurrent leaders
and reconciling total order in a deterministic way.

The multi-leader nature of Mir should lead to exceptional performance
especially on wide area networks,
but should be suitable for LAN deployments as well.

MirBFT, decouples request payload dissemination from ordering,
outputting totally ordered request digests rather than all request data.
This allows for novel methods of request dissemination.
The provided request dissemination method, however, does guarantee the availability of all request payload data.

## Compiling and running tests

The MirBFT library relies on Protocol Buffers.
The `protoc` compiler and the corresponding Go plugin need to be installed.
Moreover, some dependencies require `gcc` to be installed as well.
On Ubuntu Linux, those can be installed using

```shell
sudo snap install --classic go
sudo snap install --classic protobuf
sudo apt install gcc
```

Once instaled, the Protocol Buffer files need to be generated by executing

```shell
go generate ./protos
```

in the `mirbft` root repository directory.
This command also has to be executed each time the `.proto` files in the `protos` folder change.

Now the tests can be run by executing

```shell
go test
```

The dependencies should be downloaded and installed automatically.

## Documentation

For a description of the design and inner workings of the library, see [MirBFT Library Architecture](/docs).

For a small demo application, see [/samples/chat-demo](/samples/chat-demo)

TODO: Write a document on how to use the library and link it here.

## Contributing

**Contributions are more than welcome!**

If you want to contribute, have a look at our [Contributor's guide](CONTRIBUTING.md)
and at the open [issues](https://github.com/hyperledger-labs/mirbft/issues).
If you have any questions (specific or general),
do not hesitate to post them on [MirBFT's Rocket.Chat channel](https://chat.hyperledger.org/channel/mirbft).
You can also drop an email to the active maintainer(s).

### Public Bi-Weekly Community Call

There is a public community call once every two weeks.
The current status, any issues, future plans, and anything relevant to the project will be discussed.
Whether you have any questions that you want to ask or you have a proposal to discuss, or whether you just want to listen in, feel free to join!

Meeting information:
- Time: Tuesdays in the even weeks (wrt. week number in the calendar year), between 09:00 GMT and 09:40 GMT
- Join link: [https://us05web.zoom.us/j/82410342226?pwd=bmxnOXBxZnRUN2dyTGVWQk16RW9JUT09](https://us05web.zoom.us/j/82410342226?pwd=bmxnOXBxZnRUN2dyTGVWQk16RW9JUT09)
- Meeting ID: 824 1034 2226
- Passcode: HQG5z5
- Upcoming calls:
  * Nov 30th 2021
  * Dec 14th 2021

## Summary of references

- Public Rocket.Chat channel: https://chat.hyperledger.org/channel/mirbft
- Hyperledger Labs page: https://labs.hyperledger.org/labs/mir-bft.html
- Paper describing the algorithm: https://arxiv.org/abs/1906.05552
- Original PBFT paper: https://www.microsoft.com/en-us/research/wp-content/uploads/2017/01/p398-castro-bft-tocs.pdf

## Active maintainer(s)

- [Matej Pavlovic](https://github.com/matejpavlovic) (matopavlovic@gmail.com)

## Initial committers

- [Jason Yellick](https://github.com/jyellick)
- [Matej Pavlovic](https://github.com/matejpavlovic)
- [Chrysoula Stathakopoulou](https://github.com/stchrysa)
- [Marko Vukolic](https://github.com/vukolic)

## Sponsor

[Angelo de Caro](https://github.com/adecaro) (adc@zurich.ibm.com).

## License

The MirBFT library source code is made available under the Apache License, version 2.0 (Apache-2.0), located in the
[LICENSE file](LICENSE).

## Acknowledgments

This work has been supported in part by the European Union's Horizon 2020 research and innovation programme under grant agreement No. 780477 PRIViLEDGE.
