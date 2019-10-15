# Overview

The todo class is a re-implementation of the todo class that is a part of the FreeCAD DraftGui module.

github: [https://github.com/FreeCAD/FreeCAD/blob/master/src/Mod/Draft/DraftGui.py](https://github.com/FreeCAD/FreeCAD/blob/master/src/Mod/Draft/DraftGui.py)

It has been reimplemented here to eliminate unnecessary code and to facilitate re-implementation for more generic support, as the current implementation relies on PySide / QT's QTimer class.

# API

## Methods

### delay()
    todo.delay(function, arg)
todo.delay() calls `function` passing it `arg` using `PySide.QtCore.QTimer.singleShot()`.

# Example

    from pivy_trackers.support.todo import todo

    def my_func():
        print('hello from the delayed function!')

    todo.delay(my_func)
