# 01. Philosophy

## Why call it message-oriented?

This project uses the term Message Orientated Design to avoid confusion with what is commonly called object-oriented programming today.

The center of this model is not classes, inheritance, or getters and setters.

The center is a set of independent stateful entities that cooperate through messages without reaching directly into one another's internals.

## Basic model

Each object is treated as a state machine.

    Object = State + Message handling + State transition

An object decides its own behavior and state transition from its current state and the message it receives.

    (Current State, Incoming Message)
        ->
    (Next State, Outgoing Messages)

This is a conceptual model. It does not require every implementation to be written as a pure function.

## Boundary

The most important boundary in this design is:

    Between objects = Message
    Inside an object = Function Call

An object must not request work from another object by directly invoking that object's internal function.

Ordinary function calls are allowed inside an object. A Message Receptor converts an incoming external message into an internal function call.

## Inheritance

Inheritance is not a requirement of Message Orientated Design.

If different objects can interpret the same message in their own ways, polymorphic behavior does not require a shared parent class.

Inheritance is not forbidden, but using inheritance is not evidence that a design is message-oriented. Any dependency on a parent class's internal state or implementation must be considered separately if it weakens object independence.

## Goal

The goal is to preserve local ownership of state and responsibility even as a system becomes very large, while making cross-boundary dependencies explicit as messages.