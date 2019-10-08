# Getting Started

## Installing

Installation is straightforward.  Simply clone the project into a path visible through your project's top-level module:

    cd /my/project/top/module/path
    git clone https://github.com/joelgraff/pivy_trackers.git

Accessing pivy_trackers classes, then, makes it easy as a top-level import:

    from pivy_trackers.base import Base

## Key Concepts
***
### Scenegraph Management
Pivy_trackers provides a Python developer with an easy way to directly manipulate the Coin3D scenegraph by generating specific scenegraph node structures which are then inserted and accessed though the pivy_tracker classes.

Check out the [[Scenegraph]] documentation to learn more.
***
### Traits

Traits are 'atomic' tracker features which encapsulate one or several scenegraph nodes and related functions.  By inheriting specific traits in a custom pivy_tracker class, specific features / functions can be implemented a la carte (node picking / selection, dragging, geometry, styling, and input events for example).

Check out the [[traits]] documentation to learn more.
***
### Layered Complexity

Pivy trackers are also designed to work in layers of complexity.  A basic tracker might be a MarkerTracker or LineTracker (both included by default in the library).  However, custom tracker classes may be built that may contain any number of these trackers or modify default selection / dragging / styling behaviors accordingly.  

Check out the [custom classes](Customizing) documentation to learn more.
***
## Limitations

Pivy_trackers depends on pivy - a library of Python bindings for Coin3D developed specifically for the FreeCAD project.  While pivy may be used independently of FreeCAD, it's valid use cases are entirely limited to FreeCAD itself.  Pivy_trackers endeavors to exist as a library solely dependent on pivy.  However, as no alternative projects exist which depend upon pivy, there are certain FreeCAD dependencies which still exist in pivy_trackers.  These dependencies, however, can be mitigated if and when use cases outside FreeCAD arise.