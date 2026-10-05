# 05. Hierarchy and Domain Managers

Message Manager and Domain Manager have different roles.

- **Message Manager:** delivers Messages.
- **Domain Manager:** makes decisions specific to a domain.

A complex entity can be split:

    Dog
    ├─ Dog Brain
    └─ Dog Moving

Dog Brain and Dog Moving exchange Messages through Dog Manager instead of directly calling each other's functions.

When another domain owns required information, ask that domain by Message.

    Physical Manager
        ↓ request
    Material Manager
        ↓ response
    Physical Manager

The basic rule is: **ask the owner of the state for the information or decision instead of reading that state directly**.
