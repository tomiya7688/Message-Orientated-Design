# 03. Message Sender and Message Receptor

## Every object has a communication boundary

Each object has a Message Sender and a Message Receptor as its boundary with the outside world.

    Incoming Message
          |
          v
    Message Receptor
          |
          v
    Object internal functions / state machine
          |
          v
    Message Sender
          |
          v
    Outgoing Message

## Responsibilities of the Message Receptor

The Message Receptor has deliberately limited responsibilities.

1. Receive a message addressed to the object.
2. Identify the message kind.
3. Invoke the corresponding internal function.

For example, suppose dog's Receptor receives:

    owner, dog, move, 100, 0

The Receptor invokes the internal function corresponding to the move message:

    move_request(owner, 100, 0)

This is the point where an ordinary function call begins.

## What the Receptor does not do

The Receptor does not make semantic decisions such as:

- whether 100, 0 is a valid value;
- whether the dog can move in its current state;
- whether owner is allowed to request the move;
- what should be sent on success or failure.

Those decisions belong to the called processing function, such as move_request.

The Receptor is the conversion boundary from a message to an internal function call, not a place for domain logic.

## Responsibilities of the Message Sender

The Message Sender is the object's exit point for messages.

Instead of directly invoking another object's functions, it emits a message containing the sender, recipient, message kind, arguments, and any other required fields.

If a request is invalid, the rejection is also sent through the Sender as a message when a response is required.