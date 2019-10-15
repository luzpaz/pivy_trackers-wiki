# Overview

The Event trait class provides event callback support to nodes in the scenegraph.  Event callbacks may be global (responding to any event of the appropriate type), or *pathed* such that they respond only to events which occur on a specific scenegraph node path.

"Pathed" events prevent callbacks from being triggered unless a specific node (typically `SoMarkerSet` or `SoLineSet`) is clicked.  This provides overall efficiency where large numbers of interactive geometry / trackers are generated and it is recommended as the default way to implement a callback.  If a global callback is required, consider using the [ViewState](view_state) class event callback methods to apply callbacks at the view level.

# API

## Prototypes

The following attributes are prototypes for Base members:

    base = None
    view_state = None
    mouse_state = None
    name = ''

## Static Attributes

    Event._self_weak_list = []
A list of weak references to event objects for pathing

    Event._default_callback_node = None
A callback node used for global event updates

## Static Methods

    Event.set_paths()
Used to set paths on event nodes which have been flagged as requiring an event path

## Attributes

### event
### event.callbacks
### callbacks
### path_nodes
## Methods

### __init__()
    self.__init__(self):
Generates the CoinGroup structure for the Event trait, establishes singleton global callbacks for mouse state updates, and prepares the class for callback handling and pathing

### _event_mouse_event()
    def _event_mouse_event(self, data, event_cb)
Internal class event callback for updating mouse state

### _event_button_event()
    def _event_button_event(self, data, event_cb)
Internal class event callback for updating button state

# Example




    def add_event_callback_node(self):
        """
        Add an event callback node to the current group
        """

        self.event.callbacks.append(
            self.event.add_node(Nodes.EVENT_CB, 'EVENT_CALLBACK')
        )

        self.callbacks.append({})

    def remove_event_callback_node(self, node):
        """
        Remove an event callback node from the current group
        """

        if node not in self.event.callbacks:
            return

        self.event.remove_node(node)

        _index = self.event.callbacks.index(node)

        del self.event.callbacks[_index]
        del self.callbacks[_index]

    def set_event_paths(self):
        """
        Set the specified path on the event callback at the specified index
        """

        if not self.path_nodes:
            return

        if len(self.event.callbacks) < len(self.path_nodes):
            return

        for _i, _node in enumerate(self.path_nodes):
            _node = self.path_nodes[_i]
            _sa = coin_utils.search(_node, self.view_state.sg_root)
            self.event.callbacks[_i].setPath(_sa.getPath())

    def add_event_callback(self, event_type, callback, index=-1):
        """
        Add an event callback
        """

        #if none exist, add a new one
        #otherwise default behavior reuses last-created SoEventCb node
        if not self.event.callbacks:
            print(self.name, 'adding event cb node')
            self.add_event_callback_node()

        _et = event_type.getName().getString()

        if not _et in self.callbacks:
            self.callbacks[index][_et] = {}

        _cbs = self.callbacks[index][_et]

        if callback in _cbs:
            return

        _cbs[callback] = \
            self.event.callbacks[index].addEventCallback(event_type, callback)

    def remove_event_callback(self, event_type, callback, index=-1):
        """
        Remove an event callback
        """

        _et = event_type.getName().getString()

        if _et not in self.callbacks:
            return

        _cbs = self.callbacks[index][_et]

        if callback not in _cbs:
            return

        self.event.callbacks[index].removeEventCallback(
            event_type, _cbs[callback])

        del _cbs[callback]

    def add_mouse_event(self, callback):
        """
        Convenience function
        """

        self.add_event_callback(MouseEvents.LOCATION2, callback)

    def add_button_event(self, callback):
        """
        Convenience function
        """

        self.add_event_callback(MouseEvents.MOUSE_BUTTON, callback)

    def remove_mouse_event(self, callback):
        """
        Convenience function
        """

        self.remove_event_callback(MouseEvents.LOCATION2, callback)

    def remove_button_event(self, callback):
        """
        Convenience function
        """

        self.remove_event_callback(MouseEvents.MOUSE_BUTTON, callback)

    def events_enabled(self):
        """
        Returns whether or not event switch is on
        """

        return self.event.whichChild == 0

    def toggle_event_callbacks(self):
        """
        Switch event callbacks on / off
        """
        #PyLint doesn't detect getValue()
        #pylint: disable=no-member

        if self.event.whichChild.getValue() == 0:
            self.event.whichChild = -1

        else:
            self.event.whichChild = 0

    def set_event_path(self, event_type, message, verbose=False, node=None):
        """
        Add / remove path for event callbacks
        """

        if node is None:
            node = self.base.path_node

        if node is None:
            self.event.callback.setPath(self.base.path_node)
            return

        self.event.callback.setPath(self.base.path_node(node))