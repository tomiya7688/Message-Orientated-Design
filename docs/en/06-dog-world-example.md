# 06. Dog / Animal / Physical / Material Example

Example: Dog Brain requests movement.

    Dog Brain
        ↓ move
    Dog Manager
        ↓
    Dog Moving
        ↓ animal_move_request
    Animal Manager
        ↓ physical_move_request
    Physical Manager
        ↓ material query
    Material Manager
        ↓ material result
    Physical Manager
        ↓ result
    Animal Manager
        ↓
    Dog Manager

Responsibilities are separated:

- **Dog Moving:** movement processing inside Dog.
- **Animal Manager:** animal-specific decisions.
- **Physical Manager:** physical behavior.
- **Material Manager:** information and decisions about walls, poles, and other material entities.

Every boundary is crossed with Messages, not direct access to internal state or internal functions.
