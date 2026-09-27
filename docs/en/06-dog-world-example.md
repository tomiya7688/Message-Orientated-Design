# 06. Dog / Animal / Physical / Material Example

This chapter shows the principles as one end-to-end flow.

## 1. A request inside Dog

Suppose Dog Brain decides that the dog should move.

Dog Brain does not directly invoke a Dog Moving function.

    Dog Brain
        | move request
        v
    Dog Manager
        |
        v
    Dog Moving Receptor
        |
        v
    move_request(...)

Dog Moving's Receptor only identifies the message and invokes the corresponding internal function.

## 2. Result from Dog Moving

Dog Moving calculates a movement candidate using state inside the Dog domain.

It does not decide by itself whether that candidate can actually occur in the world. It sends a message to the next domain that must judge it.

    Dog Moving
        | movement candidate
        v
    Dog Manager
        |
        v
    Animal Manager

## 3. Animal-specific judgment

Animal Manager handles constraints specific to animals.

For example, body condition or other animal-level restrictions belong to the Animal domain.

Once those conditions are handled, the request can be expressed as a physical movement request and sent to Physical Manager.

    Animal Manager
        | physical movement request
        v
    Physical Manager

## 4. Physical queries Material

Suppose Physical Manager needs information about walls or utility poles to perform collision handling.

Physical Manager does not directly inspect Material's internal data.

    Physical Manager
        | material information request
        v
    Material Manager
        | material information response
        v
    Physical Manager

Material Manager responds using the Material-domain state it owns.

## 5. Physical result

Physical Manager uses the returned information to determine physical behavior and returns the result as a message.

As needed, the result travels back across domain boundaries as messages: Physical -> Animal -> Dog.

## Overall flow

    Dog Brain
        |
        v
    Dog Manager
        |
        v
    Dog Moving
        |
        v
    Animal Manager
        |
        v
    Physical Manager
        | request
        v
    Material Manager
        | response
        v
    Physical Manager
        |
        v
    Animal Manager
        |
        v
    Dog Manager

The important point is that every boundary is crossed by messages rather than direct access to another entity's internal functions or internal state.