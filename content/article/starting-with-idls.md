---
title: "Starting With IDLs"
author:  "Adam Hawkins"
date: 2021-03-14T22:29:23-10:00
draft: true
---

So you want to start using some like [protobuf][] or [thrift][]. Smart
choice. These IDL (Interface Definition Language) projects are useful
tools for building networked services. They offer things that hand
rolling HTTP+JSON (or whatever the flavor of the day is) do not. 

The first being they are statically typed and generate code. They may
combined with RPC frameworks (like gPRC) to handle client and servers.
No more writing clients and servers to ingest and ouput data. No more
arguing over bikeshedding "well designed JSON". I think these are good
things becuase it removes cognitive load from the networking layer and
frees it up for use in the application layer.

The second is coarse grained validation. I say coarse because IDLs
offer you guarantees around types and the shape of incoming data. You
can declare required fields in structs and their types. Clients and
server can only generate messages that are well types. Sure you'll
still need to higher level semantic validation. Nevertheless, all
actors in the system can rest assured based on fundamental assumptions
about the messages they recieve.

Teams and engineers don't start with these tools however. They adopt
them after using something else, then looking for an alternative.
This pior experience skews the perspective on these tools because the
same working knowledge doesn't apply.

Here's some questions to consider when starting with IDLs:

* How are IDL files (i.e. `.proto`) consumed?
* What are the best practices for writing the interfaces?
* How is client and server code generated and consumed?
* Will all services in the system share the same IDL?
* How do we release a new version?
* How do we support old clients?
* Can we use these like internal domain objects?
* What's the compatibility matrix across all the tools in the stack?
* What telemetry is provided by generated clients and servers?

[protobuf]: https://developers.google.com/protocol-buffers/
[thrift]: https://thrift.apache.org
[grpc]: https://grpc.io
