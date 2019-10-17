# Overview

The LineTracker class provides a fully-interactive single Line (or series of lines).  If more than one line is defined (i.e., more than two coordinates or multiple coordinate sets are specified), all lines are highlighted / selected as a group.

Refer to the diagram for the [LineTracker scenegraph structure](scenegraph#line-tracker-structure) for more information.

# API 

## Dependencies

The LineTracker class inherits the [GeometryTracker](GeometryTracker) class.

## Attributes

### line
    line = self.geometry.add_node(coin_enums.NodeTypes.LINE_SET, name)
Reference to the coin `SoLineSet` node

## Methods

### __init__()
    __init__(self, name, points, parent, view=None)
Initializes the LineTracker, applying the list of points (in tuple form) to the underlying `SoCoordinate3` node.

# Example
**(requires FreeCAD-specific module dependencies)**

    import FreeCADGui as Gui

    from pivy_trackers.tracker.context_tracker import ContextTracker
    from pivy_trackers.tracker.line_tracker import LineTracker


    class MyLineTracker(ContextTracker):

        def __init__(self):

            super().__init__('MyLineTracker', Gui.ActiveDocument.ActiveView)

            self.line_tracker = \
                LineTracker('line_tracer', [(0.0, 0.0, 0.0), (100.0, 100.0, 0.0)], self.base)

            self.set_visibility()
            self.insert_into_scenegraph(True)
    