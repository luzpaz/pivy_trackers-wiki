# Overview

CoinStyles.Style provides constant Style instances which define parameters for `SoDrawStyle`, `SoBaseColor`, and `SoMarkerSet` classes to create a comprehensive way to describe a geometry style.

A custom style may be built off of an existing basic style, or created from scratch by specifying the appropriate parameters on creation.

# API

## Attributes

### id (String)
    self.id = 'my style'
Name of style

### style (Integer)
    self.style = coin.SoDrawStyle.FILLED
Style value for SoDrawStyle class

### shape (String)
    self.shape='CIRCLE_FILLED'
Name and fill style for `SoMarkerSet` rendering, corresponding to [coin_enums.MarkerStyles](coin_enums-MarkerStyles) naming.

### line_wdith (Float)
    self.line_width = 1.0
Width of lines for `SoLineSet`

### line_pattern (Integer / hex)
    self.line_pattern = 0x0f0f
Line pattern, specified in hex.  0 = pixel off, f = pixel on

### size (Integer)
    self.size = 7
Size of `SoMarkerSet` node, valid values are 5, 7, and 9.

### color (tuple(float, float, float))
    self.color = (1.0, 0.5, 0.25)
Color for `SoBaseColor` node in RGB format, value ranges [0.0, 1.0]

## Methods

### __init__()
    __init__(self, style_id, style=coin.SoDrawStyle.FILLED,
             shape='CIRCLE_FILLED', line_width=0.0, point_size=0.0,
             line_pattern=0xffff, size=9, color=(1.0, 1.0, 1.0))

Constructor requires only a style_id be specified, providing a name for the style.

## Example

    from pivy_trackers.coincoin_styles import CoinStyles as Styles

    _style = Styles.Style('my_style', 'dashed', color=Styles.Color.GREEN)
