# Overview

The GeometryTracker class is a basic tracker implementation for creating a fully-featured tracker.  The implementation is straightforward and is intended as a superclass for inheritance in a custom tracker.

Refer to the diagram for the [GeometryTracker scenegraph structure](scenegraph#geometry-tracker-structure) for more information.

# API

## Dependencies
The GeoemtryTracker class inherits the [Base](Base-Trait), [Style](Style-Trait), [Event](Event-Trait), [Pick](Pick-Trait), [Select](Select-Trait), and [Geometry](Geometry-Trait) traits.

## Attributes

None

## Methods

### add_node_events()
    add_node_events(self, node=None, add_callback=False, pathed=True)
Add `SoEventCallback` nodes and Select trait callback references to the graph.
Must be called by the inheriting class to enable node events.

Parameters:
* node - a reference to the geometry node.  Required if applying event pathing.
* add_callback - add a `SoEventCallback` node to the graph.  Useful only if a path is applied.
* pathed - Enforce event pathing.  Forced to true if `add_callback` is True.

# Example

    from .trait.coin.coin_enums import NodeTypes as Nodes
    from .geometry_tracker import GeometryTracker

    class MyMarkerTracker(GeometryTracker):

        def __init__(self, name, point):

            super().__init__(name=name, parent=parent)

            #build node structure for the tracker
            self.marker = self.geometry.add_node(Nodes.MARKER_SET, name)

            self.set_style()
            self.set_visibility(True)
            self.update(self.point)
