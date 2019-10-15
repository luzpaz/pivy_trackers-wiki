# Overview

The PublisherEvents class provides event definitions to be used in tandem with the [Publisher](Publisher-Trait) and [Subscriber](Subscriber-Trait) trait classes.  Together, these classes form an inter-object messaging system modeled on the well-documented publisher / subscriber pattern.

PublisherEvents defines events categorized by various UI / object layers.

That is, an event is described as part of a layer, which encapsulates a portion of the application in some form.  For example, there may be task-level events, or events triggered by changes in geometry, or changes at the tracker level.

Which each of these layers, specific events are defined.  Events are generated as powers-of-two, enabling them to be compounded by bitwise operations.
