# 04. Message Manager

A Message Manager is responsible **only for delivery**.

    Sender -> Message Manager -> Target Receptor

It:

- checks the destination;
- delivers locally when the target is in scope;
- passes the Message upward when the target is outside the scope.

It does not make domain decisions.

Local communication should stay local. It does not need to pass through a Global Manager.

    Dog Brain
        ↓
    Dog Manager
        ↓
    Dog Moving

A Message should pass through only the minimum management scope required for delivery.
