# 05. Hierarchy and Domain Managers

## Message Manager and Domain Manager

This document distinguishes two kinds of manager responsibilities.

### Message Manager

Responsible for message delivery. It does not interpret domain semantics.

### Domain Manager

An object responsible for decisions, coordination, or state specific to a domain. A Domain Manager communicates by messages just like any other object.

## Splitting a complex object

If a Dog becomes complex, all behavior does not need to be forced into one enormous Dog object.

For example:

    Dog
      - Dog Brain
      - Dog Moving
      - ...

Dog Brain and Dog Moving do not directly invoke each other's internal functions. They exchange messages through Dog Manager.

## Passing work to a higher domain

Even if Dog Moving calculates a movement candidate, that does not mean the movement is valid in the world.

Responsibility can be passed upward from dog-specific processing into more general domains.

    Dog domain
        |
        v
    Animal domain
        |
        v
    Physical domain

Animal Manager handles animal-specific conditions. Physical Manager handles physical behavior.

The higher the level, the less it depends on dog-specific details and the more it handles rules of a broader domain.

## Querying another domain

If Physical Manager needs information about a wall, utility pole, or other material object, it does not directly read Material's internal state.

It sends a request message to Material Manager. Material Manager uses the state owned by its domain and returns a response message.

    Physical Manager
        | request
        v
    Material Manager
        | response
        v
    Physical Manager

This preserves the boundary between the owner of state and the entity that needs information derived from that state.

## Key principle

    Do not directly inspect state owned by another domain.
    Request the information or decision from the entity that owns that domain through a message.