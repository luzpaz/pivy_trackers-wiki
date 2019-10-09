# Technical Overview

Pivy_trackers is a modular system where a custom tracker can be built by inheriting one or more core 'traits' or basic tracker classes to create a custom tracker with just the right set of features. Using this approach makes designing a tracker and it's accompanying scene structure easy - review the provided [tutorials] and [examples] for more information.

Pivy_trackers manages this modularity by using the Python Method Resolution Order (MRO) rules to it's advantage.  Specifically, each "trait" generates a scenegraph structure which provides specific functionality (like events, styles, geometry, and selection) that is to be plugged into the larger scenegraph structure that represents the tracker.

Because traits are the most basic element of trackers, each trait, itself, does not inherit another class.  Nor do traits obey the rules object inheritance as they're commonly understood in object-oriented programming.  That is, while a Tracker class inherits it's traits directly, each trait, itself, inherits no other classes, though it may rely on the features provided by another trait.

As an example,  let's suppose we have a tracker which inherits the Base and Event traits as follows:

`class MyTracker(Base, Event):`

The Event trait class depends on certain attributes of the Base trait class be present in order to successfully initialize (for example, the Event trait depends on the Base trait attributes, `base`, `view_state`, `mouse_state`, and `name`). 
 Because of this, traits which depend on other traits must be listed later in the MRO than their dependencies. This approach also means that each trait must not pass on control to the next class in the MRO until it has first added it's own features to the tracker class instance.  That is, each trait does not call `super().__init__()` until the very end of it's own `__init__()` method.

As a result, subsequent trait classes which depend upon others will access class members that do not exist at design time.  While this poses no real problem for Python, it does make for a more complicated approach to class design for the programmer.  To simplify matters (and keep the IDE's python linter happy) trait classes with dependencies declare 'prototypes' of the class members which are added at runtime.  These prototype declarations and definitions may be found at the top of each trait class as static class members.

This underlying prototyping mechanism, however, should pose no issue for developing custom tracker classes.  At the tracker level, normal inheritance rules apply.  Simply declare the trait classes from which the tracker will inherit, and call `super().__init()` *first* to ensure the trait features are added to the tracker object before other initialization processes take place.

