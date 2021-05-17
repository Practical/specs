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


Structs
~~~~~~~

#. A literal ``S``.
#. If the struct is namespace or otherwise scoped, the scope's representation follows.
#. Next comes the **total** length, in decimal, of the struct's data.
#. The struct's name.
#. 8 characters encoding the hash of the struct's content.

Struct Hash Encoding
^^^^^^^^^^^^^^^^^^^^

The struct's hash value is calculated over it's name and members according to the following formula:

**TBD**

If a struct indirectly points back to itself (e.g. contains a pointer to itself), the inner struct reports a fixed hash value of
``0x2bcdadbd0483cb7c``.

The hash is calculated in 64 bits.

The lower 48 bits of the hash are taken, and then encoded with Base64 with ``+`` replaced with ``_`` and ``/`` replaced with ``@``.
On platforms where ``@`` cannot be used, another symbol MUST be used for that specific platform. On platforms where no second
character is available, the ABI SHOULD use Base63 (47.8 bits). It MAY use Base32 (40 bits). It MAY also use plain hexadecimal
representation with upper case letters (32 bits).
