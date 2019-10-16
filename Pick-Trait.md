# Overview

The Pick trait adds the `SoPickStyle` node to the tracker graph.  The node is added directly to the [Base](Base-Trait) trait graph's `top` node.

The Pick trait exists largely to enable / disable node picking in the scene graph.  By default, node picking is enabled, thus the pick trait is not necessary unless it is desirable to make nodes unpickable.

# API

## Dependencies

The Pick trait depends on the [Base](Base-Trait) trait.

## Prototypes

The following prototypes from [Base](Base-Trait) are defined:

    base

## Attributes

### pick
    pick = self.base.add_node(coin_enums.NodeTypes.PICK_STYLE, 'Pick_Style')
Reference to the `SoPickStyle` node added directly to `base.top`.

## Methods

### __init__()
    __init__(self)
Construct the class, creating the `SoPickStyle` node and adding it to the base graph.

### set_pick_style()
    set_pick_style(self, is_pickable)
Sets the pick style for the `SoPickStyle` node to either `coin_enums.PickStyles.PICKABLE` or `coin_enums.PickStyles.UNPICKABLE`.

### is_pickable()
    is_pickable(self)
Returns whether or not the Pick trait has enabled node picking.

# Example

    from pivy_trackers.trait.base import Base
    from pivy_trackers.trait.pick import Pick

    class my_pick_tracker(Base, Pick):

        def __init__(self):
            
            super().__init__(name='my_pick_tracker')
  
            #disable picking.  Picking is enabled by default, with or without Pick trait.
            self.set_pick_style(False)
