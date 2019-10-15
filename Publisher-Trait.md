# Overview

The Publisher class is used in tandem with the [Subscriber class](subscriber_events) to provide object-level event notification and handling.  This level of communication happens strictly within Python, apart from Coin3D and enables interaction between tracker objects, as well as UI elements.

Object-level events make it possible to update UI controls (like text boxes) based on changes which occur in a tracker, or vice-versa.

The publisher / subscriber pattern is well-documented and used here with a custom event definition class, [PublisherEvents](publisher_events)

# API

## Attributes

### counter (Static)
    Publisher.counter = 0
Class-level counter provided for unique ID naming

### event_callbacks
    self.event_callbacks = {}
Dictionary containing references to callbacks to which the object may dispatch event notifications.
The dictionary consists of nested dictionaries of callbacks.  Each sub-dictionary is keyed to the event type as defined in PublisherEvents.  Each callback is keyed to it's own reference in the sub-dictionary.

### pub_id
    self.pub_id = Publisher.counter
Default id value for each Publisher instance

## Methods

### __init__()
    Publisher.__init__(self):
Initializes the publisher class attributes, incrementing the class counter.

### get_subscribers()
    self.get_subscribers(self, events = 0)
Returns a list all callbacks registered for the specified events.  Events can be compounded by bit-wise AND operations.

### register()
    self.register(self, who, events, callback=None)
Registers `who` for notification of `events` by triggering `callback`.
`events` may be a list of events.
`callback` may be None, in which case, it is assumed `who` has a method named `notify()`

### unregister()
   self.unregister(self, who, events)
Unregisters `who` from `events`.

### dispatch()
    self.dispatch(self, event, message, verbose=False)
Dispatches `message` to the events indicated by `event`.  If `verbose`, dispatch outputs who is sending what on which events.

# Example

    self.register(listener, my_event)
    self.dispatch(my_event, ('My message', my_message_object))

