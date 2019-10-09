# Scenegraph Structures

This section goes into detail about the scenegraph node structures generated and maintained by the pivy_trackers classes.  If you are unfamiliar with scenegraphs and how they work, it will be helpful to develop at least a general understanding.  

A few links of general information:

* [WebGL scenegraph fundamentals](https://webglfundamentals.org/webgl/lessons/webgl-scene-graph.html)
* [gamedev.net explanation](http://archive.gamedev.net/archive/reference/programming/features/scenegraph/index.html)
* [StackOverflow question](https://stackoverflow.com/questions/5319282/game-engines-what-are-scene-graphs)


Additionally, links to the Coin3D documentation for referenced scenegraph nodes:

* SoLineSet
* SoMarkerSet
* SoEventCb
* SoSwitch
* SoGroup
* SoBaseColor
* SoDrawStyle
* SoSeparator
* SoFcSelection
* SoPickStyle

Most of the [[traits]] in pivy_trackers create a corresponding scenegraph node structure to provide it's functionality.

Included here is a list of each trait (and the base tracker classes) and their corresponding scenegraph node structures

## CoinGroup

The CoinGroup class lies at the heart of the pviy-tracker traits and trackers.  This class provdies the base node structure
for each trait / tracker and determines whether or not the effects of the trait / tracker may be felt beyond
their sibling / child nodes as well as making them switchable to enable / disable the effect of their nodes.

A CoinGroup object  scenegraph node structure consists of one or two of the following nodes:

Swtich | Group | Separator 
-------|-------|----------
[[images/switch.svg]] | [[images/group.svg]] | [[images/separator.svg]]

Specifically, a CoinGroup may be any one of these nodes individually, or a combination of a Swtich node and a Group or Separator node.
The Switch node may also act as the parent or child of the group / separator node.

## Trait Structures
---
### Base Structure

The Base trait creates a switched separator:

[[images/switch-separator.svg]]

This node structure provides the greatest control and safety, making it switched, so it can or cannot be traversed,
as well as separated - insulating the remainder of the scenegraph from it's effects.
---
### Drag Structure

 NOT YET IMPLEMENTED
---
### Event Structure

The Event trait adds a switched group, allowing it's effects to influence siblings of it's parent switch.
This node structure may consist of one or more SoEventCallback nodes, which provide node-level input event notification
for keyboard, mice, and other devices.


[[images/event.svg]]
---
### Geometry Structure

The Geometry trait adds a simple group with a SoTransform and SoCoordinate3 node.  Thus transformations applied
to the geometry node will also be aplpied to subsequent sibling / child geometry nodes


[[images/geometry.svg]]

---
### Pick Structure

The Pick trait adds an SoPickStyle node to the base node group, thus it's a child of the Base SoSeparator node.


[[images/pick.svg]]

---
### Select Structure

The Select trait adds a SoFCSelection node (FreeCAD-specific) to the base node group separator.


[[images/select.svg]]

---
### Style Structure

The Style trait adds a SoGroup node with SoBaseColor and SoDrawStyle nodes as immediate children
Thus, effects of these nodes are applied to all siblings and children following it's traversal

## Trackers
---
### Geometry Tracker Structure
---
### Marker Tracker Structure
---
### Line Tracker Structure