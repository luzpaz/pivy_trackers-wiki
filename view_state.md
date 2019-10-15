# Overview

The ViewState class is a [Singleton](singleton) class which provides state tracking for the view in which trackers are generated.

The ViewState class provides a number of view-related services, including triggering input callbacks at the view level (global), accessing QT UI panels, and performing matrix transformations on data points.

# API

## Attributes

### _matrix
    ViewState()._matrix = None
A reference to the last view matrix retrieved by the view state.

### active_task_panel
    ViewState().active_task_panel = None
FreeCAD-specific attribute which provides a reference to the UI task panel currently open

### callbacks
    ViewState().callbacks = {}
A dictionary of callbacks, keyed to the node event class to which they belong (`SoKeyboardEvent`, `SoLocation2Event', `SoMouseButtonEvent`)
### sg_root
    ViewState().sg_root = ViewState().view.getSceneGraph()
A reference to the scenegraph root, here relying on the FreeCAD InventorView class

### view
    ViewState().view = None
A reference to the active application view

### viewport
    ViewState().viewport = view.getViewer().getSoRenderManager().getViewportRegion()
A reference to the application render viewport

## Methods

### add_button_event()
    ViewState().add_button_event(self, callback)
Convenience function to add a mouse button event callback

### add_event_cb()
    ViewState().add_event_cb(self, callback, event_class)
Add a callback to the specified event class

### add_mouse_event()
    ViewState().add_mouse_event(self, callback)
Convenience function to add a mouse movement callback

### get_active_task_panel()
    ViewState().get_active_task_panel(self, refresh=False)
Retrieve a reference to the active task panel.  Refresh forces a lookup using `getMainWindow().findChild()`

### get_matrix()
    ViewState().get_matrix(self, node, parent=None, refresh=True)
Retrives the transformation matrix applied to `node`.  If `parent` is undefined, scenegraph root is assumed.  Refresh forces an update of the matrix if True, returns last-retrieved matrix if False.

### getCursorPos()
    ViewState().getCursorPos(self)
Convenience function to get the cursor position

### getObjectInfo()
    ViewState().getObjectInfo(self, pos)
Convenience function to get object info under mouse cursor

### getPoint()
    ViewState().getPoint(self, pos)
Convenience function to get the world coordinates at the specified screen coordinates

### getPointOnScreen()
    ViewState().getPointOnScreen(self, point)
Convenience function to get the screen coordinates at the specified world coordinates

### remove_button_event()
    ViewState().remove_button_event(self, callback)
Convenience function to remove a `SoMouseButton` event callback

### remove_event_cb()
    ViewState().remove_event_cb(self, callback, event_class)
Remove a callback from the specified event class

### remove_mouse_event()
    ViewState().remove_mouse_event(self, callback)
Convenience function to remove a `SoLocation2` event callback

### transform_points()
    ViewState().transform_points(self, points, node=None, refresh=True)
Transforms supplied list of iterable point data.  If node is specified and refresh is True, the transformation matrix will be updated before transformation.  Otherwise, the previous matrix will be used.

Returns the transformed points

# Example

    from pivy_trackers.support.view_state import ViewState

    def mouse_event(self, user_data, event_cb)
        print('callback for {}'.format(str(event_cb.getClassTypeId()))

    def button_event(self, user_data, event_cb)
        print('callback for {}'.format(str(event_cb.getClassTypeId()))

    view_state.add_mouse_event(mouse_event)
    view_state.add_button_event(button_event)