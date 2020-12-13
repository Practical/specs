****************************
Application Binary Interface
****************************

Name Mangling
=============

Functions
---------

Function mangled name is composed of the following sequence:

#. A literal ``_P``
#. Function name encoding:
    #. Number of characters in the function's base name
    #. The function's base name, verbatim
#. Function's return type
    #. A literal ``R``
    #. mangled name of return type
    #. A literal ``E``
#. Function's parameters
    #. A literal ``P``
    #. All positional parameters' mangled type name in sequence.
    #. A literal ``E``

Types
-----

Modifiers
~~~~~~~~~

* Mutable types have a prefix ``m``
* Reference types begin with ``r``

Scalar (built-in) types
~~~~~~~~~~~~~~~~~~~~~~~

Built-in types mangle according to the following table:

+------------------+------------------------------------------------------+
| Type             | Mangled name                                         |
+==================+======================================================+
| Void             | ``v``                                                |
+------------------+------------------------------------------------------+
| Bool             | ``b``                                                |
+------------------+------------------------------------------------------+
| Signed integer   | ``s`` followed by number of bytes (``S8`` is ``s1``) |
+------------------+------------------------------------------------------+
| Unsigned integer | ``u`` followed by number of bytes                    |
+------------------+------------------------------------------------------+
| Character        | ``c`` followed by number of bytes                    |
+------------------+------------------------------------------------------+

Pointers
~~~~~~~~

Pointer type is mangled as ``p`` followed by the pointed to type mangling

Arrays
~~~~~~

#. A literal ``A``
#. Number signifying the array's dimensions
#. Mangled name of element type

