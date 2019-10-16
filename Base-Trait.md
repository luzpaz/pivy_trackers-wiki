# Overview

The Base trait provides common core features for other traits:

* [Publisher](Publisher-Trait) / [Subscriber](Subscriber-Trait) notifications
* [ViewState](view_state) and [MouseState](mouse_state) singletons
* A core [coinGroup structure](Scenegraph#coin_group)
* Scenegraph node management convenience wrappers

# API

The API is composed of the following sections:

* [Prototypes](Base-Trait#Prototypes)
* [Class Statics](Base-Trait#Statics)
* [Class Attributes](Base-Trait#Attributes)
* [Class Methods](Base-Trait#Methods)

## Dependencies

None.  The Base Trait inherits the [Publisher](Publisher-Trait) and [Subscriber](Subscriber-Trait).

## Prototypes

None

### set_style()
    set_style(self, style=None, draw=None, color=None)
Overridden by the Style trait, if inherited.

## Statics

### view_state
    base.view_state = ViewState()
Provides access to the ViewState singleton in the view_state module

### mouse_state
    base.mouse_state = MouseState()
Provides access to the MouseState singleton in the mouse_state module

## Attributes

### base
    self.base = CoinGroup(
        is_separator=True, is_switched=True,
        name=self.name + '_base', parent=parent)
Default [scenegraph node structure](scenegraph#base-structure)

### name
    self.base.name = self.names[0]
The tracker name derived from `base.names`

### names
    self.base.names = name.split('.')[::-1]
List of names used to name the tracker.  Names is typically composed of three elements:  Document name, object name, and tracker name, separated by periods.  Document and Object names are names for the parent document and object, which are needed by the Select trait (specifically, the FreeCAD coin3D class `FCSelection`).  Thus, when defining the base node, pass the name parameter as:

    'document_name.object_name.tracker_name'

The last name is always the tracker name, regardless of how many names are passed.  Name order is reversed in the list after parsing.

### path_node
    self.path_node = None
Node to be assigned by the [Select trait](Select-trait) for path-constrained events.  This is used to ensure input events do not trigger callbacks unless a specific node is picked.

### sg_root
    self.base.sg_root = self.view_state.sg_root
The root node of the entire scenegraph structure.  Also exposed in the `ViewState` class as `ViewState().sg_root`

### transform
    self.transform = base.add_node(Nodes.TRANSFORM, 'Transform')
Reference to a coin `SoTransformNode` at the top of the node structure.  Useful for applying transformations to all geometry.

### top, root
    self.top = base.top
    self.root = base.root
Convenience attributes for access to the top / root nodes of the [CoinGroup](coin_group) structure referenced by the 'base' attribute.

## Methods

### __init__()
    Base.__init__(self, name, parent=None)
Class constructor.  Requires `name` as a string.  Names may have up to three parts, delimited by a period (.).  The last name is considered the name for the tracker object itself.  Optional `parent` is passed to the underlying [CoinGroup](coin_group) instance.

### finalize()
    self.finalize(self, node=None, parent=None)
Finalize the object and corresponding graph structure, removing it from the scenegraph

### insert_into_scenegraph()
    self.insert_into_scenegraph(self, verbose=False)
Insert the base node into the scenegraph

**verbose** - Boolean (False).  Indicates whether or not the scenegraph node structure should be dumped to the console.

Insertion into an active scenegraph needs to occur outside of scenegraph traversals.  To accomplish this, the [todo] class is employed.  The internal function [_do_insert](Base-Trait#_do_insert) is passed as the function to call for insertion.

### _do_insert()
    self._do_insert(self)
Callback for 'todo.delay' method used in 'insert_into_scenegraph'.  In this method, the root node of the CoinGroup created for the base trait is inserted as an immediate child of the scenegraph root.  [Event](Event-Trait) pathing is also triggered, establishing paths for specified geometry and their corresponding SoEventCallback nodes.

### copy()
    self.copy()
Wrapper for [CoinGroup.copy()](coin_group#copy).  Copies a graph structure.

### insert_group()
    self.insert_group(self, coin_group)
Wrapper for [CoinGroup.insert_group()](coin_group#insert_group). Inserts the graph of a CoinGroup as a child of the current graph.

### is_visible()
    self.is_visible(self)
Wrapper for [CoinGroup.is_visible()](coin_group#is_visible).  Returns True / False indicating graph visibility for graphs with a `SoSwitch` node.

### set_visibility()
    self.set_visibility(self, visible=True)
Wrapper for [CoinGroup.set_visibility()](coin_group#set_visibility).  Enables / disables visibility for graphs with a `SoSwitch` node.

## Example

Create an instance of the Base trait class, defining it's name and inserting it into the scenegraph

    from pivy_trackers.base import Base

    def base_trait_example():

        #Create the Base trait class instance
        base_trait = Base(name='DocumentName.ObjectName.MyTracker')

        #set the trait visibility
        base_trait.set_visibility(False)

        #insert the graph into the main scenegraph
        base_trait.insert_into_scenegraph()