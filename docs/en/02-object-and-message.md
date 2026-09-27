# 02. Objects and Messages

## A message is not a function call

A Message in this design is not merely another syntax for a function call.

For example, the following information itself is a message:

    owner, dog, move, 100, 0

Conceptually, it contains:

    from = owner
    to = dog
    message = move
    arguments = [100, 0]

The sender does not need to know how to invoke a move function on dog. It only needs to express that it wants to send a move message to dog.

## Sender and recipient identities

A message must at least identify its logical sender and recipient.

This lets the receiver consider not only what was requested but also who requested it, and it also makes the response destination explicit.

The from and to fields are logical identities or addresses. Cryptographic signatures and authentication mechanisms are not specified yet.

## Responses are messages too

A response that crosses an object boundary is not modeled as a function return value.

Whether a request succeeds or fails, any required response is sent as a new message through the Message Sender.

Example:

    owner -> dog : move 100 0

On success:

    dog -> owner : move-accepted

On rejection:

    dog -> owner : move-rejected ...

The exact response messages are part of each domain's design.

## State owned by another domain

An object does not directly read state owned by another object or domain.

When information is needed, it sends a request message to the entity that owns that information and receives the result as a message.