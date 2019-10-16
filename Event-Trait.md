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
    event = CoinGroup(switch_first=True, is_separator=False, is_switched=True,
                      parent=self.base, name=self.name + '__EVENTS')
Refers to the CoinGroup object containing the `SoEventCallback` nodes

### event.callbacks
    event.callbacks = []
List of references to `SoEventCallback` nodes which have been added to this Event trait instance

### callbacks
    callbacks = []
List of references to Python callback functions which have been added to this Event trait instance

### path_nodes
    path_nodes = []
List of references to coin `SoNode` objects which provide the target path for a `SoEVentCallback` node to be triggered.  These must be rendered nodes, like `SoMarkerSet` or `SoLineSet`.  If multiple `SoEventCallback` nodes exist, do not have the same path (or have no paths), a separate reference in the `path_nodes` list must exist, corresponding to the relevant `SoEventCallback` node.  Where there are fewer path node references that callback node references, the last path node in the list is used for all remaining callback nodes.  See the [example](Event-Trait#Example) for details.

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

### add_button_event()
    add_button_event(self, callback):
Convenience function to add a mouse button (`SoMouseButtonEvent`) event callback to the `events` group

### add_event_callback()
    add_event_callback(self, event_type, callback, index=-1)
Adds a callback to the last-created `SoEventCallback` node.  If none exist, one is created.

* event_type - The class of the event to be created <br>(e.g. `coin.SoLocation2Event.getClassTypeId()` or `coin_enums.MouseEvents.LOCATION2`)
* callback - A reference to the Python callback function
* index - Index of the `SoEventCallback`node to which the callback should be added.  If -1, the last-created node is used.

### add_event_callback_node()
    add_event_callback_node(self)
Adds a `SoEventCallback` node to the group node referenced by `event`.  Use `add_event_callback` to add callbacks to the Event class trait.

### add_mouse_event()
    add_mouse_event(self, callback)
Convenience function to add a mouse (`SoLocation2Event`) event callback to the `events` group

### events_enabled
    events_enabled(self)
Returns whether or not event switch has enabled the event callback nodes

### remove_button_event()
    remove_button_event(self, callback)
Convenience function to remove a mouse (`SoMouseButtonEvent`) event callback from the `events` group

### remove_event_callback()
    remove_event_callback(self, event_type, callback, index=-1)
Remove an event callback.  Removes the corresponding node if all callbacks are deleted.

### remove_event_callback_node()
    remove_event_callback_node(self, index)
Remove the `SoEventCallback` node from the `event` group at `index`.  Use `remove_event_callback()` to remove callbacks instead.

### remove_mouse_event()
    remove_mouse_event(self, callback)
Convenience function to remove a mouse (`SoLocation2Event`) event callback from the `events` group

### set_event_paths()
    set_event_paths(self)
Set paths for all `SoEventCallback` nodes.  Typically performed immediately after graph is inserted into scenegraph

### toggle_event_callbacks()
    toggle_event_callbacks(self)
Switch event callbacks on or off


# Example

    from pivy_trackers.coin.coin_enums import NodeTypes as Nodes

    from pivy_trackers.trait.base import Base
    from pivy_trackers.trait.event import Event
    from pivy_trackers.trait.geometry import Geometry

    class my_tracker(Base, Event, Geometry):

    def __init__(self):

        super().__init__(name='my_tracker', parent=None)

        #Add a mouse movement and button event callback,
        #creating a new `SoEventCallback` node automatically
        self.add_mouse_event(self.my_mouse_event)
        self.add_button_event(self.my_button_event)

        #Append None to the path_nodes array to ensure
        #the first `SoEventCallback` node is not pathed
        self.path_nodes.append(None)
        
        #Manually add a second callback node
        self.add_callback_node()

        #Add new callbacks (will be added automatically to last-created callback node)
        self.add_mouse_event(self.my_pathed_mouse_event)
        self.add_button_event(self.my_pathed_button_event)

        #Create some geometry
        _marker = self.geometry.add_node(Nodes.MARKER_SET, 'my_marker')

        #Add a reference to the geometry for creating a path
        self.path_nodes.append(_marker)

        #Place the geometry at the origin
        self.geometry.coordinate.point.setValue((0.0, 0.0, 0.0))
        

    def my_mouse_event(self, user_data, event_cb):
        print('my_mouse_event called!')

    def my_button_event(self, user_data, event_cb):
        print('my_button_event called!')

    def my_pathed_mouse_event(self, user_data, event_cb):
        print('my_pathed_mouse_event called!')

    def my_pathed_button_event(self, user_data, event_cb):
        print('my_pathed_button_event called!')

