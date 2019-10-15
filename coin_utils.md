# Overview

coin_utils provides utility functions to interact with the coin scenegraph through pivy.coin.

These utilities are managed / wrapped by other pivy_tracker classes and should generally not be necessary to use in custom tracker implementations.

# API

### describe()
    describe(node)
Returns a string describing a node and it's most relevant attributes.  Used by `coin_utils.dump_node()`

### dump_node()
    dump_node(node)
Returns a string describing the structure of `node` and it's children for console output

### search()
    search(node, parent)
Returns a `SoSearchAction` object which searches for `node` in `parent`.

### remove_child()
    remove_child(node, parent)
Removes `node` from `parent`.  Removal is delayed to avoid conflict with scenegraph traversals

### insert_child()
    insert_child(node, parent, index=-1)
Inserts `nod` into `parent`.  If `index` is non-negative, `node` will be inserted before the node at `index` in `parent`.

### add_child()
    add_child(node_class, parent, name='')
Adds a child node of type `node_class` to `parent`, named as `name`.  If `name` is empty, the string identifier for `node_class` is substituted.

For valid parents, uses `insert_child` to delay insertion pending graph traversals.

# Example

    from pivy_trackers.coin import coin_utils as utils
    from pivy_trackers.coin.coin_enums import NodeTypes as Nodes

    my_parent = utils.add_child(Nodes.GROUP, None, 'Parent')
    my_child = utils.add_child(Nodes.TRANSFORM, my_parent, 'Transform')
    utils.dump_node(my_parent)