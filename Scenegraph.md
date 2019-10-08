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

## Coin Group

[[images/Untitled_1.svg]]

## Trait Structures

### Base Structure

### Drag Structure

### Event Structure

### Geometry Structure

### Pick Structure

### Select Structure

### Style Structure

## Trackers

### Geometry Tracker Structure

### Marker Tracker Structure

### Line Tracker Structure