*********
Operators
*********

Precedence
==========

.. tabularcolumns:: |L|C|L|

.. csv-table::
    :header: 1, 2, 3

    1, 2, 3
    very very long, very very long, very very long

.. tabularcolumns:: |L|C|L|

+----------------+----------------+----------------+
| Head 1         | Head 2         | Head 3         |
+================+================+================+
| 1              |              2 | 3              |
+----------------+----------------+----------------+
| very very long | very very long | very very long |
+----------------+----------------+----------------+

.. tabularcolumns:: |L|C|L|C|L|

.. csv-table::
    :header: Precedence, Operator, Description, Associativity

    "1 (highest)", ``::``, "Scope resolution", "None"

    2, ``++``, "Postfix increment", Left-to-right
    , ``--`` , Postfix decrement
    , ``()`` , Function call
    , ``[]`` , Array/Slice subscripting
    , ``.`` , Struct member selection (lvalue)
    , ``->`` , Struct member selection (pointer)
    , ``expect!type`` , Safe cast (explicit implicit cast)
    , ``cast!type`` , Static cast
    , ``const_cast!type`` , CV removal cast
    , ``reinterpret_cast!type`` ,

    3 , ``++`` , Prefix increment , Right-to-left
    , ``--`` , Prefix decrement
    , ``+`` , Unary plus
    , ``-`` , Unary minus
    , ``~`` , Bitwise NOT (One's complement)
    , ``!`` , Logical NOT
    , ``*`` , Pointer dereference
    , ``&`` , Address-of

    4 ,,,, Reserved

    5 , ``*`` , Multiplication , Left-to-right
    , ``/`` , Division
    , ``%`` , Modulo (remainder)
    , ``&`` , Bitwise AND ,, Higher priority than C++

    6 , ``+`` , Addition , Left-to-right
    , ``-`` , Subtraction
    , ``|`` , Bitwise OR ,, Higher priority than C++
    , ``^`` , Bitwise XOR ,, Higher priority than C++

    7 , ``<<`` , Left shift , Left-to-right
    , ``>>`` , Right shift

    8 , ``<`` , Less than , Left-to-right
    , ``<=`` , Less than or equals
    , ``>`` , Greater than
    , ``>=`` , Greater than or equals

    9 , ``==`` , Equals , Left-to-right
    , ``!=`` , Not equals

    10 , ``&&`` , Logical AND , Left-to-right

    11 , ``||``, Logical OR , Left-to-right

    12 , ``=`` , Assignement , Right-to-left
    , ``+=`` , Additive assignment
    , ``-=`` , Subtractive assignment ,
    , ``*=`` , Multiplicative assignment
    , ``/=`` , Division assignment
    , ``%=`` , Modulo assignment
    , ``<<=`` , Left shift assignment
    , ``>>=`` , Right shift assignment
    , ``&=`` , Bitwise AND assignment
    , ``^=`` , Bitwise XOS assignment
    , ``|=`` , Bitwise OR assignment

Remarks
=======



