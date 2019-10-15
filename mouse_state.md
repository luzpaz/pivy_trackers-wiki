# Overview

MouseState maintains state tracking for mouse clicks, movement and dragging.  ButtonState is a helper class used by MouseState

MouseState is implemented as a [Singleton](singleton) to provide a globally-accessible state object.

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
# Example