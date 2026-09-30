# 00. Origins of Object Orientation

## Purpose of this chapter

Message Orientated Design is not merely a different name for the design techniques commonly called object-oriented programming today.

The historical starting point used by this project is the line of thought strongly expressed by Alan Kay and early Smalltalk: **independent entities protect their internals and interact through messages**.

This project is not a historical reimplementation of early Smalltalk, nor does it claim to turn Alan Kay's work directly into a specification. It takes that historical direction as a starting point and develops its own rules for modern, large-scale software design.

## The early idea

In *The Early History of Smalltalk*, Alan Kay describes an approach to large-scale systems using a biological analogy: protected universal “cells” interacting only through messages.

The important point is that the center of the idea was not simply bundling data with procedures. It was **communication between entities with boundaries**.

In 1998, Kay again emphasized that Smalltalk was not about its syntax or class library, and not even fundamentally about classes. He described messaging as the central idea.

This project therefore treats the following as its historical starting point:

- an entity owns its internal state;
- other entities do not directly manipulate that state;
- interaction between entities occurs through messages;
- the receiving entity decides how to interpret a message and how to behave;
- in large systems, communication boundaries matter more than exposing internal structure.

## Distinction from common modern object orientation

Today, “object-oriented programming” is often explained through classes, inheritance, interfaces, encapsulation, and polymorphism.

Those can be useful techniques, but they are not the center of this project.

Inheritance, in particular, is not a requirement of Message Orientated Design. If different entities can interpret the same message in their own ways, polymorphic behavior does not require a common parent class.

For that reason, this repository does not simply use the phrase “original object orientation”. To avoid confusion with the modern conventional meaning of object orientation, it uses the separate name **Message Orientated Design**.

## Do not confuse history with this specification

The historical material explains the inspiration for this design.

This repository does **not** claim that Alan Kay or Smalltalk directly specified the concrete rules used here, such as Message Sender, Message Receptor, hierarchical Message Managers, Domain Managers, or immutable Messages.

Those are design mechanisms introduced by this project to apply a message-centered model to large systems.

## References

- Alan C. Kay, *The Early History of Smalltalk*: https://archive.computerhistory.org/resources/access/text/2024/06/102739394-05-0001-acc.pdf
- Alan Kay, “prototypes vs classes was: Re: Sun's HotSpot”, Squeak mailing list, 1998: https://lists.squeakfoundation.org/pipermail/squeak-dev/1998-October/017019.html
- Computer History Museum, *Introducing the Smalltalk Zoo*: https://computerhistory.org/blog/introducing-the-smalltalk-zoo-48-years-of-smalltalk-history-at-chm/
