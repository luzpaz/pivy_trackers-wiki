# Overview

The Select trait is specific to FreeCAD and enables node selection behaviors in the coin scenegraph for use in FreeCAD event callbacks by adding the `SoFCSelection` node to the graph structure.

This custom coin-based FreeCAD node provides selection and event services for the FreeCAD GUI view classes and is used in updating the MouseState, among other miscellaneous purposes.

Two instance-specific callbacks are provided to manage object-specific selection state management as well as minimal global state management

# API

## Dependencies

The Select trait depends upon the [Base](Base-Trait), [Style](Style-Trait), and [Event](Event-Trait) traits.

## Prototypes

The following prototypes from Base, Style, and Event are defined:

    #Base Prototypes
    base
    mouse_state
    name
    names

    #Style Prototypes
    coin_style
    set_style(self, style=None, draw=None, color=None)

    #Event Prototypes
    event

## Static members

    #Reference to the node that is currently highlighted.
    highlight_node = None

    #List of currently selected elements.
    selected = []

## Attributes

### handle_events
    handle_events = True
Boolean indicating whether or not events are handled (sunk) with this callback.  Set to False to allow `SoEventCallback` nodes later in the graph traversal to also receive these events

### select
    select = coin.SoType.fromName("SoFCSelection").createInstance()
Reference to `SoFCSelection` node inserted directly into the graph's `base.top` group.

## Methods

### __init__()
    __init__(self)
Object initialization.  Adds `SoFCSelection` node to graph

### do_multi_select()
    do_multi_select(self)
Performs multi-selection.  Called internally from Select event callbacks.

### do_single_select()
    do_single_select(self)
Performs single-selection.  Called internally from Select event callbacks.

### is_selected()
    is_selected(self)
Returns boolean indicating whether or not tracker is selected.

### select_button_event()
    select_button_event(self, user_data, event_cb)
Select `SoMouseButtonEvent` callback

### select_mouse_event()
    select_mouse_event(self, user_data, event_cb)
Select `SoLocation2` event callback

### update_highlight()
    update_highlight(self)
Updates object highlighting on mouse over.  Called internally from Select event callbacks.


# Example

    from pivy_trackers.trait.base import Base
    from pivy_trackers.trait.event import Event
    from pivy_trackers.trait.select import Select

    class my_select_tracker(Base, Event, Select):

    def __init__(self):

        super().__init__(name='my_tracker', parent=None)

        #Create some geometry
        self.marker = MarkerTracker(name='my_marker', point=(0.0, 0.0, 0.0), parent=self.base)
        self.line = LineTracker(name='my_line', point=[(0.0, 0.0, 0.0), (100.0, 100.0, 100.0)], parent=self.base)
