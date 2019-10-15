# Overview

MarkerStyles provides constant enumerants for the various styles which may be applied to the coin3D `SoMarkerSet` node class.  These enumerants directly store the integer value which represents the marker type and size that is assigned to the `SoMarkerSet.markerIndex` property.

Additionally, static methods are provided to facilitate constructing the marker index integer by providing the type name and size as separate values (string and integer, respectively).

Marker styles consist of 20 different types:

    CROSS, PLUS, MINUS, SLASH, BACKSLASH, BAR, STAR, Y, LIGHTNING, WELL, CIRCLE, SQUARE, DIAMOND, TRIANGLE, RHOMBUS,  HOURGLASS, SATELLITE, PINE_TREE, CAUTION, SHIP

The latter 10 types (CIRCLE through SHIP) have alternate LINE and FILLED representations.

Additionally, all marker style types may have one of three sizes: 5, 7, and 9.

# API

## Methods

### get()
    MarkerStyles.get(shape, size)
Returns the enumerant based on the passed shape (String) and size (Integer) parameters.

### get_by_value()
    MarkerStyles.get_by_value(value)
Returns the enumerant name based on the passed integer value which represents the `SoMarkerSet.markerIndex` value.

**Note:**
*These methods are static members of a Const class, though they do not employ the @staticmethod decoration

## Enumerants

    CROSS_5 = coin.SoMarkerSet.CROSS_5_5
    PLUS_5 = coin.SoMarkerSet.PLUS_5_5
    MINUS_5 = coin.SoMarkerSet.MINUS_5_5
    SLASH_5 = coin.SoMarkerSet.SLASH_5_5
    BACKSLASH_5 = coin.SoMarkerSet.BACKSLASH_5_5
    BAR_5 = coin.SoMarkerSet.BAR_5_5
    STAR_5 = coin.SoMarkerSet.STAR_5_5
    Y_5 = coin.SoMarkerSet.Y_5_5
    LIGHTNING_5 = coin.SoMarkerSet.LIGHTNING_5_5
    WELL_5 = coin.SoMarkerSet.WELL_5_5
    CIRCLE_LINE_5 = coin.SoMarkerSet.CIRCLE_LINE_5_5
    SQUARE_LINE_5 = coin.SoMarkerSet.SQUARE_LINE_5_5
    DIAMOND_LINE_5 = coin.SoMarkerSet.DIAMOND_LINE_5_5
    TRIANGLE_LINE_5 = coin.SoMarkerSet.TRIANGLE_LINE_5_5
    RHOMBUS_LINE_5 = coin.SoMarkerSet.RHOMBUS_LINE_5_5
    HOURGLASS_LINE_5 = coin.SoMarkerSet.HOURGLASS_LINE_5_5
    SATELLITE_LINE_5 = coin.SoMarkerSet.SATELLITE_LINE_5_5
    PINE_TREE_LINE_5 = coin.SoMarkerSet.PINE_TREE_LINE_5_5
    CAUTION_LINE_5 = coin.SoMarkerSet.CAUTION_LINE_5_5
    SHIP_LINE_5 = coin.SoMarkerSet.SHIP_LINE_5_5
    CIRCLE_FILLED_5 = coin.SoMarkerSet.CIRCLE_FILLED_5_5
    SQUARE_FILLED_5 = coin.SoMarkerSet.SQUARE_FILLED_5_5
    DIAMOND_FILLED_5 = coin.SoMarkerSet.DIAMOND_FILLED_5_5
    TRIANGLE_FILLED_5 = coin.SoMarkerSet.TRIANGLE_FILLED_5_5
    RHOMBUS_FILLED_5 = coin.SoMarkerSet.RHOMBUS_FILLED_5_5
    HOURGLASS_FILLED_5 = coin.SoMarkerSet.HOURGLASS_FILLED_5_5
    SATELLITE_FILLED_5 = coin.SoMarkerSet.SATELLITE_FILLED_5_5
    PINE_TREE_FILLED_5 = coin.SoMarkerSet.PINE_TREE_FILLED_5_5
    CAUTION_FILLED_5 = coin.SoMarkerSet.CAUTION_FILLED_5_5
    SHIP_FILLED_5 = coin.SoMarkerSet.SHIP_FILLED_5_5

    CROSS_7 = coin.SoMarkerSet.CROSS_7_7
    PLUS_7 = coin.SoMarkerSet.PLUS_7_7
    MINUS_7 = coin.SoMarkerSet.MINUS_7_7
    SLASH_7 = coin.SoMarkerSet.SLASH_7_7
    BACKSLASH_7 = coin.SoMarkerSet.BACKSLASH_7_7
    BAR_7 = coin.SoMarkerSet.BAR_7_7
    STAR_7 = coin.SoMarkerSet.STAR_7_7
    Y_7 = coin.SoMarkerSet.Y_7_7
    LIGHTNING_7 = coin.SoMarkerSet.LIGHTNING_7_7
    WELL_7 = coin.SoMarkerSet.WELL_7_7
    CIRCLE_LINE_7 = coin.SoMarkerSet.CIRCLE_LINE_7_7
    SQUARE_LINE_7 = coin.SoMarkerSet.SQUARE_LINE_7_7
    DIAMOND_LINE_7 = coin.SoMarkerSet.DIAMOND_LINE_7_7
    TRIANGLE_LINE_7 = coin.SoMarkerSet.TRIANGLE_LINE_7_7
    RHOMBUS_LINE_7 = coin.SoMarkerSet.RHOMBUS_LINE_7_7
    HOURGLASS_LINE_7 = coin.SoMarkerSet.HOURGLASS_LINE_7_7
    SATELLITE_LINE_7 = coin.SoMarkerSet.SATELLITE_LINE_7_7
    PINE_TREE_LINE_7 = coin.SoMarkerSet.PINE_TREE_LINE_7_7
    CAUTION_LINE_7 = coin.SoMarkerSet.CAUTION_LINE_7_7
    SHIP_LINE_7 = coin.SoMarkerSet.SHIP_LINE_7_7
    CIRCLE_FILLED_7 = coin.SoMarkerSet.CIRCLE_FILLED_7_7
    SQUARE_FILLED_7 = coin.SoMarkerSet.SQUARE_FILLED_7_7
    DIAMOND_FILLED_7 = coin.SoMarkerSet.DIAMOND_FILLED_7_7
    TRIANGLE_FILLED_7 = coin.SoMarkerSet.TRIANGLE_FILLED_7_7
    RHOMBUS_FILLED_7 = coin.SoMarkerSet.RHOMBUS_FILLED_7_7
    HOURGLASS_FILLED_7 = coin.SoMarkerSet.HOURGLASS_FILLED_7_7
    SATELLITE_FILLED_7 = coin.SoMarkerSet.SATELLITE_FILLED_7_7
    PINE_TREE_FILLED_7 = coin.SoMarkerSet.PINE_TREE_FILLED_7_7
    CAUTION_FILLED_7 = coin.SoMarkerSet.CAUTION_FILLED_7_7
    SHIP_FILLED_7 = coin.SoMarkerSet.SHIP_FILLED_7_7

    CROSS_9 = coin.SoMarkerSet.CROSS_9_9
    PLUS_9 = coin.SoMarkerSet.PLUS_9_9
    MINUS_9 = coin.SoMarkerSet.MINUS_9_9
    SLASH_9 = coin.SoMarkerSet.SLASH_9_9
    BACKSLASH_9 = coin.SoMarkerSet.BACKSLASH_9_9
    BAR_9 = coin.SoMarkerSet.BAR_9_9
    STAR_9 = coin.SoMarkerSet.STAR_9_9
    Y_9 = coin.SoMarkerSet.Y_9_9
    LIGHTNING_9 = coin.SoMarkerSet.LIGHTNING_9_9
    WELL_9 = coin.SoMarkerSet.WELL_9_9
    CIRCLE_LINE_9 = coin.SoMarkerSet.CIRCLE_LINE_9_9
    SQUARE_LINE_9 = coin.SoMarkerSet.SQUARE_LINE_9_9
    DIAMOND_LINE_9 = coin.SoMarkerSet.DIAMOND_LINE_9_9
    TRIANGLE_LINE_9 = coin.SoMarkerSet.TRIANGLE_LINE_9_9
    RHOMBUS_LINE_9 = coin.SoMarkerSet.RHOMBUS_LINE_9_9
    HOURGLASS_LINE_9 = coin.SoMarkerSet.HOURGLASS_LINE_9_9
    SATELLITE_LINE_9 = coin.SoMarkerSet.SATELLITE_LINE_9_9
    PINE_TREE_LINE_9 = coin.SoMarkerSet.PINE_TREE_LINE_9_9
    CAUTION_LINE_9 = coin.SoMarkerSet.CAUTION_LINE_9_9
    SHIP_LINE_9 = coin.SoMarkerSet.SHIP_LINE_9_9
    CIRCLE_FILLED_9 = coin.SoMarkerSet.CIRCLE_FILLED_9_9
    SQUARE_FILLED_9 = coin.SoMarkerSet.SQUARE_FILLED_9_9
    DIAMOND_FILLED_9 = coin.SoMarkerSet.DIAMOND_FILLED_9_9
    TRIANGLE_FILLED_9 = coin.SoMarkerSet.TRIANGLE_FILLED_9_9
    RHOMBUS_FILLED_9 = coin.SoMarkerSet.RHOMBUS_FILLED_9_9
    HOURGLASS_FILLED_9 = coin.SoMarkerSet.HOURGLASS_FILLED_9_9
    SATELLITE_FILLED_9 = coin.SoMarkerSet.SATELLITE_FILLED_9_9
    PINE_TREE_FILLED_9 = coin.SoMarkerSet.PINE_TREE_FILLED_9_9
    CAUTION_FILLED_9 = coin.SoMarkerSet.CAUTION_FILLED_9_9
    SHIP_FILLED_9
