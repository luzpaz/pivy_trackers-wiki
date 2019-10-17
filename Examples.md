v# Overview

The `pivy_tracker.examples` module contains examples of pivy trackers designed for use in FreeCAD.  Each example contains a 'command' and 'task' class module which may be used directly in a FreeCAD Python workbench.  Simply import the 'command' module class into a workbench's `init_gui.py` file to begin testing with it.  

Otherwise, the individual trackers themselves may be instanced directly from the Python console in FreeCAD as follows.  An example using the SelectDragTracker example:

    >>> from pivy_trackers.examples.select_drag.select_drag_tracker import SelectDragTracker
    >>> tracker = SelectDragTracker(Gui.ActiveDocument.ActiveView)
    >>> tracker.insert_into_scenegraph(True)

# Selection and Dragging

**Module:**<br>
    pivy_trackers.examples.select_drag

The select_drag tracker demonstrates basic tracker highlighting, selection, and dragging.  A simple box consisting of four unconnected markers and lines are created.  Mouse over each marker / line to see highlighting in action.  Click on each element (or over empty space) to select / deselect elements.  Use CTRL+Click to select / deselect multiple elements.

DRAGGING NOT YET IMPLEMENTED

# Other Examples

Other examples may be found in the Example section of the [Trackers](Modules#trackers) and [Traits](Modules#traits) classes documented in the [Module API](Modules).  Note that most examples found there are not self-contained and are, thus, not complete.