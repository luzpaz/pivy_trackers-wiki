# Overview

The Publisher class is used in tandem with the [Subscriber class](subscriber_events) to provide object-level event notification and handling.  This level of communication happens strictly within Python, apart from Coin3D and enables interaction between tracker objects, as well as UI elements.

Object-level events make it possible to update UI controls (like text boxes) based on changes which occur in a tracker, or vice-versa.

The publisher / subscriber pattern is well-documented and used here with a custom event definition class, [PublisherEvents]