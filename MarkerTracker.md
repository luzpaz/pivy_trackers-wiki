# Overview

The MarkerTracker class provides a fully-interactive single Marker (or series of markers).  If more than one marker is defined (i.e., multiple coordinates are specified), all markers are highlighted / selected as a group.

Refer to the diagram for the [MarkerTracker scenegraph structure](scenegraph#marker-tracker-structure) for more information.

# API

## Dependencies

The MarkerTracker Class inherits the [GeometryTracker](GeometryTracker) class.

## Attributes

### marker
    marker = self.geometry.add_node(coin_enums.NodeTypes.MARKER_SET, name)
Reference to the `SoMarkerSet` node in the Geometry trait graph

### point
    point = tuple()
Point (or list of points) in tuple form applied to the `geometry.coordinate` node

## Methods

### __init__()
    __init__(self, name, point, parent)
Initialize the MarkerTracker class, defining the marker point(s), it's name, and parent node.
Also ensures marker node is visible, and style is set.

### set_style()
    set_style(self, style=None, draw=None, color=None)
Overload of `Style.set_style()`, setting the coin `SoMarkerSet.markerIndex` attribute according to the value specified in `style`

### update()
    update(self, coordinates=None)
Update the coordinate values for the MarkerTracker graph

# Example
**(requires FreeCAD-specific module dependencies)**

    import FreeCADGui as Gui

    from pivy_trackers.tracker.context_tracker import ContextTracker
    from pivy_trackers.tracker.marker_tracker import MarkerTracker


    class MyMarkerTracker(ContextTracker):

        def __init__(self):

            super().__init__('MyMarkerTracker', Gui.ActiveDocument.ActiveView)

            self.marker_tracker = \
                MarkerTracker('mt', (0.0, 0.0, 0.0), self.base)

            self.set_visibility()
            self.insert_into_scenegraph(True)
    