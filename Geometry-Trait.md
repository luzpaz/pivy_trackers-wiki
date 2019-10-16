# Overview

The Geometry Trait creates a graph structure to support nodes that may be rendered onscreen (like `SoMarkerSet` and `SoLineSet`)  The graph structure itself is simple, containing a `SoTransform` and `SoCoordinate` node in a single `SoGroup`.  No actual "renderable" coin nodes are added as a part of the Geometry trait.  Rendering nodes onscreen is pushed to the [GeometryTracker](GeometryTracker) class.

Refer to the [Geometry Trait graph](scenegraph#geometry-structure) for more information.

# API

## Dependencies
The Geometry trait depends on the [Base](Base-Trait) and [Style](Style-Trait) traits.

## Prototypes
The following prototypes provided by the Base and Style traits are defined:

    base
    active_style
    name

    set_visibility()

## Attributes

### geometry
    geometry = CoinGroup(
                   is_separator=False, is_switched=False,
                   parent=self.base, name=self.name + '__GEOMETRY')
Defined as a single group without a switch, any transformations applied to the Geometry Trait are retained and applied to siblings positioned later in the graph traversal.

The geometry CoinGroup defines a `transform` (`SoTransform`) and `coordinate` (`SoCoordinate3`) node.

## Methods

### update()
    update(self, coordinates)
Base implementation for geometry updates.  Currently does nothing.

### set_coordinates()
    set_coordinates(self, coordinates=None)
Set the passed coordinates as the value(s) of the `coordinate` node.

`coordinate` may be either a single or list of, `Iterable` data structure(s).  Structures are converted to Python tuples if not already in that form.

### get()
   get(self, _dtype=tuple)
Returns a list of the coordinate value(s) stored in `coordinate` (specifically, `SoCoordinate3.point.getValues()`) as a list of iterable objects.  The type of iterable may be specified with `_dtype`.

# Example

    from pivy_trackers.trait.base import Base
    from pivy_trackers.trait.geometry import Geometry

    class my_tracker(Base, Event, Geometry):

    def __init__(self):

        super().__init__(name='my_tracker', parent=None)


        #Create some geometry
        _marker = self.geometry.add_node(Nodes.MARKER_SET, 'my_marker')

        #Place the geometry at the origin
        self.geometry.set_coordinates((0.0, 0.0, 0.0))