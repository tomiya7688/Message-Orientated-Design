# Check Policy

## Role of the checker

The checker is an auxiliary tool for determining whether a design or implementation follows Message Orientated Design.

The design principles must not be shaped around checker implementation convenience. The checker follows the principles defined by the canonical repository-level `docs/jp` documentation.

## Initial areas to check

- Does code directly invoke another object's internal function across an object boundary?
- Does code directly read or write state owned by another object or domain?
- Does external communication pass through Message Sender / Message Receptor boundaries?
- Does a Receptor contain domain decisions or semantic validation?
- Does a Receptor invoke the internal function corresponding to the received Message type?
- Is a result that crosses an object boundary represented only as a return value?
- Are required responses emitted as Messages through a Sender?
- Has domain logic been concentrated in a Message Manager that should only route Messages?
- When information from another domain is needed, is that domain queried by Message?
- Is local traffic unnecessarily routed through a Global Manager?
- Is from / to / type / content rewritten while a Message is being delivered?
- Is Manager-internal delivery identification exposed as part of the Message's semantic meaning?

## Inheritance

The checker does not accept or reject a design merely because inheritance is present or absent.

Inheritance is not the center of Message Orientated Design. The relevant question is whether implementation coupling caused by inheritance breaks entity independence or Message boundaries.

## Undecided checker details

The following have not yet been decided:

- target languages;
- static analysis approach;
- rule severities;
- configuration format;
- CI integration;
- automatic fixes;
- how Manager / Sender / Receptor roles are identified in source code.

These are checker specifications and belong in this directory rather than in the core Message Orientated Design documentation.
