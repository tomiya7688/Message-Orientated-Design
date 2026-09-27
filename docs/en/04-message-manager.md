# 04. Message Manager

## The object responsible for delivery

A Message Manager examines the message recipient and delivers the message to the target object's Message Receptor.

    Sender
      |
      v
    Message Manager
      |
      v
    Target Receptor

The Message Manager is itself an object and therefore also has a Message Sender and a Message Receptor.

## Responsibilities of a Message Manager

Its primary responsibility is delivery.

- Receive a message.
- Inspect its destination.
- If the destination is within its managed scope, deliver it to the target Receptor.
- If the destination is outside its managed scope, pass it to the required upper manager.

A Message Manager does not decide whether a dog's move is semantically valid, whether an animal can move, or whether a physical collision occurs. Those are domain decisions.

## Local communication

Internal communication does not need to pass through a Global Manager.

If Dog Brain and Dog Moving belong to the same Dog scope, their communication can be completed through Dog Manager alone.

    Dog Brain
        |
        v
    Dog Manager
        |
        v
    Dog Moving

There is no need to route that message through Animal Manager or Global Manager.

## Crossing a boundary

A message is passed upward only when it leaves the current management scope.

    Local A
       |
       v
    Upper Manager
       |
       v
    Local B

The principle is:

    A message should pass only through the minimum management scope required for delivery.

This prevents all traffic from becoming a Global Manager bottleneck. Only traffic that crosses boundaries needs higher-level routing.

## Hierarchy

Managers can be hierarchical.

A route may move upward from the sender's local manager to the common management scope shared with the destination, then downward toward the recipient.

Objects do not need to know the route. They address a message and emit it through their Sender; the manager side decides how to deliver it.