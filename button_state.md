# Overview

ButtonState is a support class for MouseState, tracking the state of mouse buttons.

# API

## Attributes

### pressed
    button.pressed = False
Sets / returns state of button press

### screen_position
    button.screen_position = ()
2-Tuple describing the screen position in pixels of the last button press

### world_position
    button.world_position = ()
3-Tuple describing the position in document units of the last button press

### dragging
    button.dragging = False
Flag indicating whether the button has been depressed as a part of a dragging operation

### drag_start
    button.drag_start = ()
Tuple indicating the start of the drag operation in world coordinates.

## Methods

### __init__()
    __init__(self)
Provides attribute initial values

### reset()
    button.reset()
Resets the button values by calling __init__()

## Example

    from pivy_trackers.support.button_state import ButtonState

   button = ButtonState()
   button.pressed = True
