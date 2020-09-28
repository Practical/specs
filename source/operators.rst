*********
Operators
*********

Precedence
==========

+-------------+---------------------------+------------------------------------+---------------+
| Precedence  | Operator                  | Description                        | Associativity |
+=============+===========================+====================================+===============+
| 1 (highest) | ``::``                    | Scope resolution                   | N/A           |
+-------------+---------------------------+------------------------------------+---------------+
| 2           | ``++``                    | Postfix increment                  | Left-to-right |
|             +---------------------------+------------------------------------+               |
|             | ``--``                    | Postfix decrement                  |               |
|             +---------------------------+------------------------------------+               |
|             | ``()``                    | Function call                      |               |
|             +---------------------------+------------------------------------+               |
|             | ``[]``                    | Array/Slice subscripting           |               |
|             +---------------------------+------------------------------------+               |
|             | ``.``                     | Struct member selection            |               |
|             +---------------------------+------------------------------------+               |
|             | ``expect!type``           | Safe cast (explicit implicit cast) |               |
|             +---------------------------+------------------------------------+               |
|             | ``cast!type``             | Static cast                        |               |
|             +---------------------------+------------------------------------+               |
|             | ``const_cast!type``       | CV removal cast                    |               |
|             +---------------------------+------------------------------------+               |
|             | ``reinterpret_cast!type`` |                                    |               |
|             +---------------------------+------------------------------------+               |
|             | ``@``                     | Pointer dereference                |               |
|             +---------------------------+------------------------------------+               |
|             | ``&``                     | Address-of                         |               |
+-------------+---------------------------+------------------------------------+---------------+
| 3           | ``++``                    | Prefix increment                   | Right-to-left |
|             +---------------------------+------------------------------------+               |
|             | ``--``                    | Prefix decrement                   |               |
|             +---------------------------+------------------------------------+               |
|             | ``+``                     | Unary plus                         |               |
|             +---------------------------+------------------------------------+               |
|             | ``-``                     | Unary minus                        |               |
|             +---------------------------+------------------------------------+               |
|             | ``~``                     | Bitwise NOT (One's complement)     |               |
|             +---------------------------+------------------------------------+               |
|             | ``!``                     | Logical NOT                        |               |
+-------------+---------------------------+------------------------------------+---------------+
| 4           | Reserved [#MmbrPtr]_                                                           |
+-------------+---------------------------+------------------------------------+---------------+
| 5           | ``*``                     | Multiplication                     | Left-to-right |
|             +---------------------------+------------------------------------+               |
|             | ``/``                     | Division                           |               |
|             +---------------------------+------------------------------------+               |
|             | ``%``                     | Modulo (remainder)                 |               |
|             +---------------------------+------------------------------------+               |
|             | ``&``                     | Bitwise AND [#Bitop]_              |               |
+-------------+---------------------------+------------------------------------+---------------+
| 6           | ``+``                     | Addition                           | Left-to-right |
|             +---------------------------+------------------------------------+               |
|             | ``-``                     | Subtraction                        |               |
|             +---------------------------+------------------------------------+               |
|             | ``|``                     | Bitwise OR [#Bitop]_               |               |
|             +---------------------------+------------------------------------+               |
|             | ``^``                     | Bitwise XOR [#Bitop]_              |               |
+-------------+---------------------------+------------------------------------+---------------+
| 7           | ``<<`` [#Shift]_          | Left shift                         | Left-to-right |
|             +---------------------------+------------------------------------+               |
|             | ``>>`` [#Shift]_          | Right shift                        |               |
+-------------+---------------------------+------------------------------------+---------------+
| 8           | ``<``                     | Less than                          | Left-to-right |
|             +---------------------------+------------------------------------+               |
|             | ``<=``                    | Less than or equals                |               |
|             +---------------------------+------------------------------------+               |
|             | ``>``                     | Greater than                       |               |
|             +---------------------------+------------------------------------+               |
|             | ``>=``                    | Greater than or equals             |               |
+-------------+---------------------------+------------------------------------+---------------+
| 9           | ``==``                    | Equals                             | Left-to-right |
|             +---------------------------+------------------------------------+               |
|             | ``!=``                    | Not equals                         |               |
+-------------+---------------------------+------------------------------------+---------------+
| 10          | ``&&``                    | Logical AND                        | Left-to-right |
+-------------+---------------------------+------------------------------------+---------------+
| 11          | ``||``                    | Logical OR                         | Left-to-right |
+-------------+---------------------------+------------------------------------+---------------+
| 12          | ``=``                     | Assignement                        | Right-to-left |
|             +---------------------------+------------------------------------+               |
|             | ``+=``                    | Additive assignment                |               |
|             +---------------------------+------------------------------------+               |
|             | ``-=``                    | Subtractive assignment             |               |
|             +---------------------------+------------------------------------+               |
|             | ``*=``                    | Multiplicative assignment          |               |
|             +---------------------------+------------------------------------+               |
|             | ``/=``                    | Division assignment                |               |
|             +---------------------------+------------------------------------+               |
|             | ``%=``                    | Modulo assignment                  |               |
|             +---------------------------+------------------------------------+               |
|             | ``<<=``                   | Left shift assignment              |               |
|             +---------------------------+------------------------------------+               |
|             | ``>>=``                   | Right shift assignment             |               |
|             +---------------------------+------------------------------------+               |
|             | ``&=``                    | Bitwise AND assignment             |               |
|             +---------------------------+------------------------------------+               |
|             | ``^=``                    | Bitwise XOS assignment             |               |
|             +---------------------------+------------------------------------+               |
|             | ``|=``                    | Bitwise OR assignment              |               |
+-------------+---------------------------+------------------------------------+---------------+

Remarks
=======


* Practical has no conditional operator (``?:``). Instead, ``if`` can be used as an expression to the same effect.
* Practical has no comma operator (``,``). Aside from being a horrible abomination, a compound expression can serve the precise
  same purpose.
* Compared to C/C++, the priority of the bitwise operations (``&``, ``|`` and ``^``) has changed. They now have a higher
  precedence than their logical counterparts, and the same precedence as their respective algebraic operations. While this might
  introduce some confusion, it is believed that 99% of expressions involving both bitwise operations and logical ones in C/C++
  either already have parenthesis around the logical ones or are bugs. As such, the (negative) impact is expected to be minimal.
* The pointer-to-method/member dereference operator does not, yet, appear in the table above. It has precedence level 4 reserved
  for it (same as C++), but that precedence, in all likelihood, represents a bug in C++. It is very likely that the final
  precedence for this operator will be 2. This seems a safer change than the bitwise operators change, as getting this one wrong
  is almost guaranteed to result in a compilation error.
* The bitwise shift operators (``<<`` and ``>>``) are only legal for unsigned integers (unless overloaded, of course). Trying to
  use them on a signed integer will result in a promotion to integer (if VRP allows it) or a compilation error.

.. rubric:: Footnotes

.. [#MmbrPtr]
    Precedence level 4 is reserved for the pointer to member/method operator. If implemented, it will likely not remain at level 4
    (as it is in C++), but rather at level 2, where it belongs.
.. [#Bitop]
    This precedence is higher than in C++
.. [#Shift]
    Defined by default only for the unsigned integer types
