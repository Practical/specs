*****
Casts
*****

Single Casts
============

A cast has source type, destination type and a weight. Optionally, the cast also has a run-time function for calculating the value
range transformation.

Each cast may be of one of three types, based on when it is allowed to invoke the cast implicitly:

+-----------------+---------------------------------------------------------------------+
| Condition name  | Meaning                                                             |
+=================+=====================================================================+
| Always          | Invocing as implicit cast is always possible                        |
+-----------------+---------------------------------------------------------------------+
| VRP Conditional | It is only possible to invoke implicitly for some Value Range cases |
+-----------------+---------------------------------------------------------------------+
| Never           | This cast is only available for explicit casts.                     |
+-----------------+---------------------------------------------------------------------+

The weight controls how likely it is, given a choice, that the compiler picks this cast over other casts, when the option is
available (see :ref:`Cast Chains`). Lower weights take precedence over higher weights. All weights *SHOULD* be higher than zero.

Weights lower than 10 are reserved for built-in casts. User defined types *SHOULD* have higher weights.

Cast Chains
===========

When tasked with converting an expression of type `srcType` to type `destType`, the compilers builds a chain of casts to achieve
this goal. The chain's length is unlimited. Built-in casts are treated the same as user defined casts. [#CppOneUDCast]_

If more than one sequence of casts is possible between `srcType` and `destTYpe`, the best one is picked based on the following
criteria, in descending order of influence:

#. Shorter chain is better
#. Lower weight is better

If two or more chains are the same lenght and have the same overall weight, a compilation error occures.

Conditional Casts
-----------------

Conditionally implicit casts participate in the chain building the same as unconditionally implicit casts. Once it is determined
that they need to be used in the chain, the VRP is calculated for them. If they are then deemed unavilable, a compilation error
occures.

This rule serves three purposes:

#. It reduces the cost of calculating the chain. Calculating the chain does not require calculating VRP for every path.
#. It allows caching of chains. In a given context, the chain from `srcType` to `destType` does not depend on the possible values
   the source expression might hold.
#. It reduces confusion. Without it, two expressions being casted with the same source and destination types might have compiled
   using two very different chains.

Explicit Casts
--------------

A chain built to fulfil an explicit cast *MAY* have the last component of type explicit only. All other components of the chain
*MUST* be either always implicit or VRP conditionally implicit.

.. [#CppOneUDCast] This is unlike C++, where the cast chain may only include one user defined cast.
