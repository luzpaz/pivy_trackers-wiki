# Overview

coin_enums provides enumerants used throughout pivy_trackers to make code more readable and to help abstract away the pivy.coin module, limiting it's use within the pivy_trackers.coin package.

Classes defined with in coin_enums inherit the [Const](const) class.

# API

The API is divided across several classes:

* [MarkerStyles](coin_enums-MarkerStyles)
* [MouseState](coin_enums-MouseState)
* [NodeTypes](coin_enums-NodeTypes)
* [PickStyles](coin_enums-PickStyles)

# Example

    form pivy_trackers.coin.coin_group import CoinGroup
    from pivy_trackers.coin.coin_enum import NodeTypes as Nodes
    from pivy_trackers.coin import coin_utils  as utils

    def create_coin_node():

        #creates a new coin3D node, adding it to the parent, if specified, and returning a reference
        my_group = utils.add_child(Nodes.SWITCH, None, 'my_switch')
