# Overview

MouseState maintains state tracking for mouse clicks, movement and dragging.  ButtonState is a helper class used by MouseState

MouseState is implemented as a [Singleton](singleton) to provide a globally-accessible state object and does not, therefore, need to be instanced apart from calling the class directly.

# API

## Attributes

### alt_down
    self.alt_down = False
Boolean indicating whether or not ALT is depressed

### button1
    self.button1 = ButtonState()
ButtonState object for the first (left) mouse button

### button2
    self.button2 = ButtonState()
ButtonState object for the second (right) mouse button

### button3
    self.button3 = ButtonState()
ButtonState object for the third (middle) mouse button

### buttons
    self.buttons = [self.button1, self.button2, self.button3]
List of ButtonState objects to facilitate iteration

### component
    self.component = ''
String name of the node under the mouse cursor (typically `SoLineSet` or `SoMarkerSet` objects)

### ctrl_down
    self.ctrl_down = False
Boolean indicating whether or not CTRL is depressed.

### object
    self.object = None
Reference to object under mouse cursor (currently unimplemented)

### screen_position
    self.screen_position = ()
2-tuple of the mouse cursor screen position in pixels

### shift_down
    self.shift_down = False

### vector
    self.vector = ()
Difference between previous world position and current world position after the mouse has moved

### world_position
    self.world_position = ()
3-tuple of the mouse cursor world position in document units

## Methods
### _udpate_button_state()
    MouseState()._update_button_state(self, arg, view_state):
Update the ButtonState() objects.  Used internally by MouseState().update()

### _update_state()
    MouseState()_update_state(self, arg, view_state):
Updates mouse key press and position information.  Used internally by MouseState().update()

### _update_component_state()
    MouseState()._update_component_state(self, info):
Update the component and object attribtues.  Used internally by MouseState().update()

### set_mouse_position()
    MouseSate().set_mouse_position(self, view_state, coord)
Force-set the position of the mouse cursor, provided a view and a coordinate location in world coordinates.
Depends on PySide.QtGui.QCursor

### update()
    update(self, arg, view_state)
Update the mouse state.

* arg - arguments returned from an SoEventCallback event either as a `dict` or as `SoEventCallback`
* view_state - current view state

Update() calls _update_state(), _update_button_state() and _update_component_state().

# Example

    import FreeCADGui as Gui
    from pivy_trackers.support.mouse_state import MouseState

    _view = Gui.ActiveDocument.ActiveView

    def mouse_event(arg):
        MouseState().update(arg, _view)

        if MouseState().button1.pressed:
        print('button1 pressed!')

    _view.addEventCallback('SoLocation2Event', mouse_event)
