# Overview

The CoinGroup class provides a base scenegraph node structure for a pivy_tracker and/or a trait.

Refer to the [CoinGroup scenegraph structures](scenegraph) documentation for a visual description of the various structures.

# API

## Attributes

### callback
References a coin `SoEventCallback` node, if defined.

### color
References a coin `SoBaseColor` node, if defined.

### coordinate
References a coin `SoCoordinate3` node, if defined.

### draw_style
References a coin `SoDrawStyle` node, if defined.

### line_set
References a coin `SoLineSet` node, if defined.

### group
References a coin `SoGroup` node, if defined.

### marker_set
References a coin `SoMarkerSet` node, if defined.

### parent
References the graph parent into which the root of the graph is inserted.

If parent is of type `CoinGroup`, the root node is inserted as a child of the `parent.top` node.
Otherwise, parent must be of `SoGroup` type.

### picker
References a coin `SoPickStyle` node, if defined.

### root
References the graph root node.  The root node is the top-most node in the graph, typically an `SoSwitch`.

### switch
References the graph `SoSwitch` node, if defined.

### top
References the `top` group node for child node additions.  This is distinct from the `root` node where the CoinGroup
contains both a switch and / or a separator node.  In this case, `top` refers to the immediate child of `root`, rather
than `root` itself.

### transform
References a coin `SoTransform` node, if defined.

## Methods

### add_node()
    add_node(self, node_class, name='')

Adds a node of the specified node class to the current CoinGroup graph using the provided name.
If name is unspecified, the coin class name is used.
Name is appended to the end of the current group name, separated by a double underscore ('__')

Returns a reference to the new node.

### copy()
    copy(self)
Returns a copy of the CoinGroup graph's `root` node

### dump()
    dump(self)
Dumps the structure of the CoinGroup to the console, starting at the `root` node

### finalize()
    finalize(self, parent=None):

Destroy the CoinGroup node graph.  If `parent` is undefined, `self.parent` is assumed.
Invalid parent results in no action.

### insert_node()
    insert_node(self, node, parent=None)

Inserts a node into the graph.  If parent is undefined, defaults to `top` node reference.

### is_visible()
    is_visible(self)
Returns a boolean indicating whether or not the graph is visible

### remove_node()
    remove_node(self, node)
Remove a node from the graph

### set_visibility()
    set_visibility(self, visible=True)
Toggles the graph's visibility setting `self.switch.whichChild` to either 0 or -1.

# Example
    from pivy_trackers.coin.coin_group import CoinGroup
    from pivy_trackers.coin.coin_enums import NodeTypes as Nodes

    group = CoinGroup(is_separator=True, is_switched=True, name='example_group1')
    group.add_node(Nodes.PICKER, 'picker')
    group.dump()