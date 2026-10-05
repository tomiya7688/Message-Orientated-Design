# 02. Objects and Messages

The minimal Message structure is:

    Message
    ├─ from
    ├─ to
    ├─ type
    └─ content

Example:

    from: owner
    to: dog
    type: move
    content:
        x: 100
        y: 0

type is the meaning of the Message. Generic kind fields such as query or request are not required. Asking for information or asking for a decision is expressed by type and content.

Messages are **immutable**. from / to / type / content are not rewritten during delivery. If a different meaning or destination is needed, create a new Message.

A global Message ID is not required. Managers may keep internal delivery IDs, but those are not semantic information for the sender or receiver.

Responses are also sent as new Messages rather than cross-object return values.
