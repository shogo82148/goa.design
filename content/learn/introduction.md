+++
title = "Introduction"
weight = 1

[menu.main]
name = "Introduction"
parent = "learn"
+++

## What is Goa?

Goa is a Go framework for writing microservices that promotes best practice by
providing a single source of truth from which server code, client code, and
documentation is derived. The code generated by Goa follows the clean
architecture pattern where composable modules are generated for the transport,
endpoint, and business logic layers. The Goa package contains middleware,
plugins, and other complementary functionality that can be leveraged in tandem
with the generated code to implement complete microservices in an efficient
manner. By using goa for developing microservices, implementers don't have to
worry about the documentation getting out of sync as Goa takes care of
generating OpenAPI specifications for HTTP based services and gRPC protocol
buffer files for gRPC based services (or both if the service supports both
transports). Reviewers and consumers can also rest assured that the
implementation follows the documentation as the code is generated from the same
source.

## Separation of Concerns

The DSL in goa v2 makes it possible to describe the services in a transport
agnostic way. The service methods DSLs each describe the method input and output
types. Transport specific DSL then describe how the method input is built from
incoming data and how the output is serialized. For example, a method may specify
that it accepts an object composed of two fields as input then the HTTP specific
DSL may specify that one of the attributes is read from the incoming request
headers while the others from the request body.

This clean decoupling means that the same service implementation can expose
endpoints accessible via multiple transports such as HTTP or gRPC. Goa takes
care of generating all the transport specific code including encoding, decoding
and validations. User code only has to focus on the actual service method
implementations.

## Basic Data Types

The primitive types include `Int`, `Int32`, `Int64`, `UInt` `UInt32`, `UInt64`,
`Float32`, `Float64` and `Bytes`. This makes it possible to support transports
such as gRPC but also makes HTTP interface definitions crisper than what JSON
allows for.

## Composable Code Generation

Code generation now follows a 2-phase process where the first phase produces a
set of writers each exposing templates that can be further modified before
running the last phase which generates the final artifacts. This makes it
possible for plugins to alter the code generated by the built-in code
generators.

## How is Goa v2 different from v1?

* Goa v2 is **composable**. The package, code generation algorithms, and
  generated code are all more modular and make fewer assumptions than Goa v1
  did.
* A microservice designed by Goa v2 is **transport-agnostic**. The decoupling of
  transport layer from the actual service implementation means that the same
  service can expose endpoints accessible via multiple transports such as HTTP
  and/or gRPC. Goa v2 takes care of generating all the transport-specific code
  including encoding, decoding, and validating requests and responses. Goa v1
  produces code for HTTP transport only.
* The generated code follows a **strict separation of concern** where the actual
  service implmentation is isolated from the transport code. User code only has
  to focus on the actual service method implementations.
* Goa v2 generates code that **relies mostly on Go standard library types**
  making it easier to interface with external code.
* The [goa-kit](https://github.com/goadesign/plugins/tree/v3/goakit) plugin makes it
  possible to generate go-kit microservices from Goa designs.