# 02. Objects and Messages

## A message is not a function call

A Message in this design is not merely another syntax for a function call.

For example, the following information itself is a message:

    owner, dog, move, 100, 0

The current minimal structure is:

    Message
    ├─ from
    ├─ to
    ├─ type
    └─ content

For example:

    from: owner
    to: dog
    type: move
    content:
        x: 100
        y: 0

The sender does not need to know how to invoke a move function on dog. It only needs to express that it wants to send a move message to dog.

## Sender and recipient identities

A message must identify its logical sender and recipient.

This lets the receiver consider not only what was requested but also who requested it, and it also makes the response destination explicit.

The from and to fields are logical identities or addresses. Cryptographic signatures and authentication mechanisms are not specified yet.

## type and content

type represents the meaning of the message understood by the receiving entity.

For example:

    type: move
    type: can_pass
    type: material_at
    type: movement_blocked

content contains the information required for that message type.

    type: move
    content:
        x: 100
        y: 0

Generic classifications such as query, decision, request, event, and result are not mandatory Message fields.

Whether a message asks for information, requests a decision, requests an action, or reports something that happened is expressed by its type and content.

For example:

    from: physical
    to: material
    type: material_at
    content:
        position: [100, 200]

is a request for information.

Whereas:

    from: physical
    to: material
    type: can_pass
    content:
        body: dog
        path: ...

asks the Material domain to make a judgment.

A Message Manager does not use such categories to make domain decisions. The responsibility for interpreting type and deciding behavior ultimately belongs to the receiving entity.

## Messages are immutable

Once a Message has been created, it is not modified.

A Manager must not rewrite from, to, type, or content while delivering it.

If a different meaning, destination, or processing stage must be expressed, a new Message is created instead of modifying the original Message.

For example:

    Dog Brain
        |
        | type: move
        v
    Dog Moving
        |
        | type: animal_move_request
        v
    Animal Manager
        |
        | type: physical_move_request
        v
    Physical Manager

does not mean that one Message is repeatedly rewritten.

Each entity creates a new Message as the result of its own judgment.

This ensures that the Message sent by the sender and the Message received by the recipient have the same contents.

## No global Message ID

The Message itself does not require a system-wide Message ID.

Information such as which numbered message it was at issuance or which numbered message it was when passing through a Manager is normally not meaningful to the sending or receiving entity.

If needed for implementation purposes, a Manager may associate its own internal ID, queue position, timestamps, retry counts, or similar metadata with a Message inside its own management scope.

Such metadata is not part of the semantics of the Message.

    Message
        from
        to
        type
        content

    Manager Internal Metadata
        internal_id
        queue_position
        received_at
        retry_count
        ...

Manager Internal Metadata belongs to the delivery system and is normally not exposed to the sender or recipient.

Different Managers may assign different internal IDs to the same Message. Those IDs do not define the identity of the Message.

## Responses are messages too

A response that crosses an object boundary is not modeled as a function return value.

Whether a request succeeds or fails, any required response is sent as a new Message through the Message Sender.

Example:

    owner -> dog
    type: move
    content:
        x: 100
        y: 0

On success:

    dog -> owner
    type: move_accepted
    content: ...

On rejection:

    dog -> owner
    type: move_rejected
    content: ...

The basic specification also does not require a response to depend on an ID of the original Message.

When a relationship must be represented, it should primarily be expressed through the meaning and content of the Messages. Implementation-level tracking information may remain internal to Managers when needed.

## State owned by another domain

An object does not directly read state owned by another object or domain.

When information is needed, it sends a Message to the entity that owns that information and receives the result as a Message.

Where appropriate, it can be better to ask the owner of the state to make the judgment itself instead of extracting raw state and deciding elsewhere.

For example, asking:

    "Give me the list of walls"

and deciding in Physical may expose more internal state than asking the appropriate domain:

    "Can this path be passed?"

The latter can preserve the boundary around domain-owned state.