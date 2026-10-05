# 03. Message Sender / Receptor

Each object has a Sender and Receptor at its external boundary.

    Message -> Receptor -> internal function
    internal processing -> Sender -> Message

## Receptor

The Receptor only:

1. receives a Message;
2. identifies its type;
3. invokes the corresponding internal function.

Example:

    type: move
        ↓
    move_request(...)

Validation, state checks, and authorization belong to the internal processing function, not the Receptor.

## Sender

The Sender is the only exit for external Messages. It does not directly invoke another object's internal functions.
