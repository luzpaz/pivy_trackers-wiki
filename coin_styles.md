# Overview

The CoinStyles class provides style support for the coin `SoDrawStyle` node.  CoinStyles consists of static methods and constant child classes to provide named enumerants for more easily-managed style definitions.  Thus, using CoinStyles, pre-defined line and marker styles may be created for use in a tracker.

# API

The CoinStyles class consists of two constant child classes:

* [Color](coin_styles-Color)
* [Style](coin_styles-Style)

# Example

    from pivy_trackers.coin.coin_styles import CoinStyles as Styles

    #Create a custom style using the 'dashed' draw style as a template, setting the color to green
    my_style = Styles.Style('dashed', color=Styles.Color.GREEN)
