# Overview

The Base trait provides common core features for other traits:

* [Publisher](Publisher-Trait) / [Subscriber](Subscriber-Trait) notifications
* [ViewState](view_state) and [MouseState](mouse_state) singletons
* A core [coinGroup structure](Scenegraph#coingroup)
* Scenegraph node management convenience wrappers

# API

The API is composed of the following sections:

* [Prototypes](Base-Trait#ProtoTypes)
* Statics(Base-Trait#Statics)
* Class Members(Base-Trait#Members)

## Prototypes

    set_style(self, style=None, draw=None, color=None)

    Overridden by the Style trait, if inherited.

## Statics

    