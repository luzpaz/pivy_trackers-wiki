# Technical Overview

Pivy_trackers is a modular system where a custom tracker can be built by inheriting one or more core 'traits' or basic tracker classes to create a custom tracker with just the right set of features. Using this approach makes designing a tracker and it's accompanying scene structure easy - review the provided [tutorials] and [examples] for more information.

Pivy_trackers manages this modularity by using the Python Method Resolution Order (MRO) rules to it's advantage.  Specifically, each "trait" generates a scenegraph structure which provides specific functionality (like events, styles, geometry, and selection) that is to be plugged into the larger scenegraph structure that represents the tracker.

# Trackers

Trackers are the sum of their traits... and then some.

A Tracker represents a self-contained scenegraph node structure that is built using the traits it inherits.  Additionally, the tracker class may modify it's node structure for whatever customizations are necessary to implement the desired behavior.

That said, working directly with the pivy/coin API can be a bit tedious and time consuming.  As a result, some basic tracker classes have been developed to help alleviate the effort required to get up and running.  These classes are:

* [GeometryTracker](GeometryTracker)
* [MarkerTracker](MarkerTracker)
* [LineTracker](LineTracker)

*Note:* MarkerTracker and LineTracker may be instanced and used on their own.  GeometryTracker is intended to act as a base for a tracker which displays and manipulates 2D geometries.

Custom trackers may be created by simply importing the appropriate trait modules and including them as superclasses for inheritance in the custom tracker's class signature. An excerpt from the GeometryTracker class definition gives a good example:

    from .trait.base import Base
    from .trait.style import Style
    from .trait.event import Event
    from .trait.select import Select
    from .trait.geometry import Geometry

    class GeometryTracker(Base, Style, Event, Select, Geometry):
        """
        Geometry tracker base class
        """

        def __init__(self, name, parent):
            """
            Constructor
            """

            super().__init__(name=name, parent=parent)

            self.coordinates = None
            self.markers = []
            self.lines = []
            self.enforce_pathing = True
            self.coin_style = CoinStyles.DEFAULT
            self.set_style()
            self.separate_select = False

It is important to note two things:  
1. The order of the traits in the inheritance list matters (see the [Traits](Modules#Traits) documentation for details). 
2. The trait classes should be initialized before any custom initialization code is run.  That is, `super().__init__()` should be called first.

# Traits

Traits make the Tracker.

Traits are intended to provide an a la carte feature set from which a Tracker may be created using multiple inheritance. Each trait encapsulates a pre-defined scenegraph node structure as well as adding methods and attributes specific to the trait to the Tracker class object which inherits it.  Note that traits tend to be "atomic" in nature.  That is, a trait is intended to represent the most basic element of a tracker, encapsulating one, and only one, functionality.  Traits, themselves do not inherit other traits.

The trick that makes traits work is broken inheritance.  That is, even though some traits depend upon others (Select depends on Style and Event, and all depend upon Base), none inherit any of the other traits.  Rather they rely on their position in the Python Method Resolution Order (MRO) to ensure that the needed attributes supplied by other traits are present when they are initialized.

As a result, unlike the tracker classes, the trait classes pass control to the next class in the MRO last, **after** the trait class has run it's own initialization code and added it's particular methods and attributes to the tracker class object.  Citing the snippet in the [Tracker](Modules#Trackers) documentation above, we can see the GeometryTracker class inherits five traits.  Of those, all depend upon Base, Select depends upon Event and Style, and Geometry depends upon Select, hence their order in the class signature.

This is risky programming, to be sure, but it's strictly limited to the trait module initializations.  Further, to help makemitigate confusion and make the nature of trait dependencies more clear, each trait has the members it requires from other modules declared and defined as static class members.  This is a form of 'prototyping' commonly used in strictier, strongly-typed languages like C++ and Java.  The use of proptyped methods and attributes is not at all required for Python, but it serves as a good way to document class dependencies where inhertiance is not used.  It also keeps the IDE linter happy. :)
