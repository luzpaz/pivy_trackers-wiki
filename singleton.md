# Overview

The Singleton class provides a singleton class pattern for Python classes, ensuring only one instance is created and is universally accessible.

This class is used primarily for global state tracking in pivy_trackers.

# Example

    from pivy_trackers.support.singleton import Singleton

    class MySingleton(metaclass=Singleton):

        counter = 0

        def __init__(self):

           MySingleton.counter += 1

    x = MySingleton()
    print (x.counter)
  
    y = MySingleton()
    print(y.counter)