# Overview

The ContextTracker provides a 'negative selection' context for highlighting and selection of geometry-rendering trackers.  That is, because input events are typically 'pathed' (only triggering the Python callbacks if the geometry itself is specifically selected), there is no mechanism to facilitate deselecting or unhighlighting previously selected or highlighted trackers.

Thus, instancing geometry-based trackers, like [MarkerTracker](MarkerTracker) or [LineTracker](LineTracker) on their own will cause node selection and highlighting to fail.  It is recommended, therefore, that any custom tracker project create a top-level class which inherits ContextTracker.  All subsequent customized tracker classes should be instanced from within this top-level tracker class.

# API

## Dependencies

The ContextTracker class inherits the [Base](Base-Trait), [Event](Event-Trait), and [Select](Select-Trait).

## Attributes

### handle_events
    handle_events=False
The ContextTracker should never not sink / consume events

## Methods

### __init__()
    __init__(self, name, view, parent=None)
Initializes Base, Event, and Select traits and the corresponding Singleton state classes.  Also adds mouse movement and button event callbacks to provide the negative selection context.

# Example
**(requires FreeCAD-specific module dependencies)**

    import FreeCADGui as Gui

    from pivy_trackers.tracker.context_tracker import ContextTracker
    from pivy_trackers.tracker.marker_tracker import MarkerTracker


    class MyMarkerTracker(ContextTracker):

        def __init__(self):

            super().__init__('MyMarkerTracker', Gui.ActiveDocument.ActiveView)

            self.marker_tracker = \
                MarkerTracker('mt', (0.0, 0.0, 0.0), self.base)

            self.set_visibility()
            self.insert_into_scenegraph(True)