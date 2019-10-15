# Overview

CoinStyles.Color provides enumerants and static methods for managing colors for the `SoBaseColor` coin3d class.

# API

## Attributes

    BLACK = (0.0, 0.0, 0.0)
    WHITE = (1.0, 1.0, 1.0)
    RED = (1.0, 0.0, 0.0)
    GREEN = (0.0, 1.0, 0.0)
    BLUE = (0.0, 0.0, 1.0)
    YELLOW = (1.0, 1.0, 0.0)
    CYAN = (0.0, 1.0, 1.0)
    MAGENTA = (1.0, 0.0, 1.0)
    GRAY_75 = (0.75, 0.75, 0.75)

    MAROON = (0.5, 0.0, 0.0)
    FOREST = (0.0, 0.5, 0.0)
    NAVY = (0.0, 0.0, 0.5)
    OLIVE = (0.5, 0.5, 0.0)
    TEAL = (0.0, 0.5, 0.5)
    PURPLE = (0.5, 0.0, 0.5)
    GRAY_50 = (0.5, 0.5, 0.5)

    ORANGE = (1.0, 0.5, 0.0)
    GOLD = (1.0, 0.85, 0.0)

## Methods

### scale()
    CoinStyles.Color.scale(color, value)
Scale the passed color by the value in the range [0.0, 1.0]

## Example

from pivy_trackers.coin.coin_styles.CoinStyles import Color

_color = Color.scale(Color.Gold, .35)