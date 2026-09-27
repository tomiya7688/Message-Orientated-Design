# 07. Role of the Checker

## The documentation is the primary artifact

The primary artifact of this repository is the documentation that defines Message Orientated Design.

The checker is an auxiliary tool for verifying whether a design or implementation follows those principles. The design principles should not be shaped around checker implementation convenience; the checker should follow the documented principles.

## Initial areas to check

At minimum, the checker may examine questions such as:

- Does code directly invoke an internal function across an object boundary?
- Does code directly read or write state owned by another object or domain?
- Does external communication pass through Message Sender / Message Receptor boundaries?
- Does a Receptor contain domain decisions or semantic validation?
- Does the Receptor translate the received message into the appropriate internal request function?
- Is a cross-object result represented only as a function return value instead of a message?
- Are required responses emitted as messages through a Sender?
- Has domain logic been concentrated into a Message Manager that should only route messages?
- When information from another domain is needed, is that domain queried by message?
- Is local traffic unnecessarily routed through a Global Manager?

## Inheritance

The checker should not accept or reject a design merely because inheritance is present or absent.

Inheritance is not the center of this model. The relevant question is whether implementation coupling created by inheritance weakens independence and message-based boundaries.

## Undecided checker details

The target languages, static-analysis approach, rule severities, configuration format, and CI integration have not yet been decided.