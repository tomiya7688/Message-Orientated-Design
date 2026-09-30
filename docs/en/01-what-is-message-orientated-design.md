# 01. What Is Message Orientated Design?

## Definition

Message Orientated Design is a design model in which **independent stateful entities are treated as state machines and interact through actual message exchange**.

Its most basic boundary is:

    Between objects = Message
    Inside an object = Function Call

When one entity requests work from another, it does not directly invoke the other entity's internal function.

The sender emits a Message through a Message Sender. On the receiving side, a Message Receptor receives that Message and invokes the corresponding internal function.

## An object is a state machine

Each object owns its own state.

It decides its processing and state transition from the Message it receives and its current state.

Conceptually:

    (Current State, Incoming Message)
        ->
    (Next State, Outgoing Messages)

This is a conceptual model and does not require implementation as a pure function.

The important point is that decisions about state belong to the entity that owns that state.

## A Message is the communication itself

A Message is not merely a function call written with different syntax.

For example:

    from: owner
    to: dog
    type: move
    content:
        x: 100
        y: 0

is itself a Message.

The sender does not need to know about an internal move function inside dog. It only sends a Message whose meaning is move.

## Do not cross a boundary by touching internals

An object does not directly read or write another object's internal state.

When information or a decision owned by another domain is needed, a Message is sent to that domain.

Where possible, the owner of the state should be asked to make the decision instead of exporting raw data for another entity to decide with.

## Sender and Receptor

Each object has a Message Sender and a Message Receptor as its communication boundary.

The responsibilities of a Message Receptor are deliberately limited:

1. receive a Message;
2. identify its type;
3. invoke the corresponding internal function.

Semantic decisions, such as whether the content is valid or whether the request is acceptable in the current state, belong to the internal processing function called after the Receptor.

## Message Manager

A Message Manager routes a Message according to its destination.

Communication that can be completed within one management scope stays within that scope. It does not have to pass through a Global Manager.

Only Messages that cross a boundary are passed to an upper Manager, allowing routing to be hierarchical.

## Domain Manager

A Message Manager is responsible for delivery. A Domain Manager is responsible for decisions specific to a domain.

For example, Dog, Animal, Physical, and Material domains can each make only their own domain decisions and communicate with other domains through Messages when necessary.

## Messages are immutable

Once created, a Message is not rewritten.

If processing requires communication with a different meaning or destination, a new Message is created.

Delivery IDs, queue positions, retry counts, and similar information are Manager-internal metadata and are not part of the meaning of the Message itself.

## Inheritance is not central

Inheritance is not prohibited, but it is not a requirement of Message Orientated Design.

The important point is not that entities share a parent class. It is that each entity can interpret the Messages it receives for itself.

## Goal

Message Orientated Design aims to preserve, even as a system becomes very large:

- clear ownership of state;
- localized responsibility for decisions;
- explicit cross-domain dependencies represented as Messages;
- independence from other entities' internal implementations;
- a communication structure that can scale hierarchically.

The following chapters define Messages, Sender / Receptor boundaries, Managers, and hierarchy in more detail.
