# 01. What Is Message Orientated Design?

Message Orientated Design treats **independent stateful entities as state machines and restricts communication between them to Messages**.

    Between objects = Message
    Inside an object = Function Call

Five basic rules:

1. Each object owns its state.
2. Do not directly call another object's internal functions.
3. Do not directly read or write another object's internal state.
4. External interaction goes through Message Sender / Receptor boundaries.
5. The receiver decides how to interpret a Message.

Inheritance is not required. The important point is not a shared parent class, but that each entity can interpret the Messages it receives.
