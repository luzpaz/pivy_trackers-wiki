# Overview

The Style trait provides visual styling for coin3D geometry by adding `SoDrawStyle` and `SoBaseColor` nodes to the graph.

Pre-defined styles are created and managed using the [CoinStyles](coin_styles) class.

Refer to the diagram for the [Style scenegraph structure](scenegraph#style-structure) for more information.

# API

## Dependencies

The Style trait depends on the [Base](Base-Trait) trait.

## Prototypes

    #Defined in Base
    base
    name

## Attributes

### coin_style
    coin_style = CoinStyles.BASE
The default style of the node

### active_style
    active_style = CoinStyles.BASE
The style currently applied to the node

### style
   style = CoinGroup(is_separator=False, is_switched=False,
            parent=self.base, name=self.name +'__STYLE')
A reference to the Style graph structure defined as a CoinGroup.  This structure consists of a single `SoGroup` node with `SoDrawStyle` and `SoBaseColor` nodes as immediate children.

## Methods

### __init__()
    __init__(self)
Construct and initialize the class, setting default style values and creating the Style graph structure.

### set_style()
    set_style(self, style=None, draw=None, color=None)
Apply `style` to the `draw` and `color` nodes.  If `style` is `None`, the style defined in `coin_style` is used.  If `active_style` is also the passed style, nothing is done.  if `draw` or `color` are defined, `style` is applied to those nodes.  Otherwise, the style is applied to the `style.draw` and `style.color` nodes.

# Example

    from pivy_trackers.coin.coin_enums import NodeTypes as Nodes
    from pivy_trackers.coin.coin_styles import CoinStyles as Styles

    from pivy_trackers.trait.base import Base
    from pivy_trackers.trait.event import Event
    from pivy_trackers.trait.style import Style
    from pivy_trackers.trait.geometry import Geometry

    class my_tracker(Base, Event, Style, Geometry):

    def __init__(self):

        super().__init__(name='my_tracker', parent=None)

        #Add a mouse movement and button event callback,
        #creating a new `SoEventCallback` node automatically
        self.add_mouse_event(self.my_mouse_event)
        self.add_button_event(self.my_button_event)

        #Create some geometry
        self.geometry.add_node(Nodes.LINE_SET, 'my_marker')

        #Add a reference to the geometry for creating a path
       self.path_nodes.append(_marker)

        #Place the geometry at the origin
        self.geometry.set_coordinates([(0.0, 0.0, 0.0), (100.0, 100.0, 0.0)])

    def my_mouse_event(self, user_data, event_cb):

       #abort if the object is currently selected
       if self.active_style == Styles.DASHED:
           return
 
       #highlight if mouse moves over object, revert to default if not
       if self.mouse_state.component == self.name:
           self.set_style(Styles.SELECTED)
       else:
           self.set_style()

    def my_button_event(self, user_data, event_cb):
        
        #toggle selection styles
        if self.active_style == Styles.DASHED:
            self.set_style()
        else:
            self.set_style(Styles.DASHED)
