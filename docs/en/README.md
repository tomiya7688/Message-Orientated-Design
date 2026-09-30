# English Documentation

The Japanese documentation in docs/jp is the canonical specification for Message Orientated Design.

The files in this directory are English translations corresponding to the Japanese originals. If the Japanese and English versions differ, the Japanese version takes precedence.

## Start here

- [00. Origins of Object Orientation](00-object-orientation-origins.md)
- [01. What Is Message Orientated Design?](01-what-is-message-orientated-design.md)

The first chapter explains the historical ideas that form the starting point of this design.

The second defines Message Orientated Design as specified by this project. Historical Smalltalk and this project's specification are deliberately kept distinct.

## Design specification

- [02. Objects and Messages](02-object-and-message.md)
- [03. Message Sender and Message Receptor](03-sender-and-receptor.md)
- [04. Message Manager](04-message-manager.md)
- [05. Hierarchy and Domain Managers](05-hierarchy-and-domain-managers.md)
- [06. Dog / Animal / Physical / Material Example](06-dog-world-example.md)

## Checker

Checker rules and implementation details are separated from the core design specification.

- [Message Orientated Design Checker](../../message-orientated-design-checker/docs/en/README.md)

The checker is an auxiliary tool that follows this specification. Checker implementation convenience must not define the core Message Orientated Design principles.

## Current status

These documents capture only the design principles agreed so far. Undecided implementation details such as transport protocols, persistence, concurrency, and cryptographic mechanisms are intentionally left unspecified.
