# Overview

Const provides inheritable Const-ness for Python classes.  Used primarily in pivy_trackers to provide classes of enumerants and static methods or other constant reference objects.

# API

The Const module contains two classes:  MetaConst and Const.  

MetaConst is used internally.  Classes should only inherit Const.

# Example

    from pivy_trackers.support.const import Const

    MyPythonConstClass(Const)

    OBJECT_NAME = 'Holy Hand Grenade'
    OBJECT_COUNT_BEFORE_THROWING = 3

Const does not enforce Const-ness beyond the class itself.  Thus, any object references within the const class must be either primitive types or class objects which inherit Const to maintain immutability.