******
Syntax
******

Grammar
=======

Introduction
------------

In this section, the following convention is used:

+---------------+-----------+--------------+
| Element       | Form      | Example      |
+===============+===========+==============+
| Non-Terminal  | Italics   | *Expression* |
+---------------+-----------+--------------+
| Verbatim text | Monospace | ``if``       |
+---------------+-----------+--------------+
| Terminal      | Bold      | **literal**  |
+---------------+-----------+--------------+

Syntax Description
------------------

*Module* :math:`\rightarrow` *GlobalExpressionsList*

*GlobalExpressionsList* :math:`\rightarrow` :math:`\epsilon`

*GlobalExpressionList* :math:`\rightarrow` *GlobalExpressionList* *GlobalExpression*

*GlobalExpression* :math:`\rightarrow` *FuncDef*

*GlobalExpression* :math:`\rightarrow` *FuncDecl*

*GlobalExpression* :math:`\rightarrow` *StructDef*

*FuncDef* :math:`\rightarrow` ``def`` *FuncDeclBody* *Statement*

*FuncDef* :math:`\rightarrow` ``def`` *FuncDeclBody* *Expression*

*FuncDecl* :math:`\rightarrow` ``decl`` *FuncDeclBody* ``;``

*FuncDecl* :math:`\rightarrow` ``decl`` ``(`` **literal_string** ``)`` *FuncDeclBody* ``;``

*FuncDeclBody* :math:`\rightarrow` *Identifier* ``(`` *FuncDeclArgs* ``)`` *FuncDeclRet*

*FuncDeclArgs* :math:`\rightarrow` :math:`\epsilon`

*FuncDeclArgs* :math:`\rightarrow` *FuncDeclArgsNonEmpty*

*FuncDeclArgsNonEmpty* :math:`\rightarrow` *FuncDeclArg*

*FuncDeclArgsNonEmpty* :math:`\rightarrow` *FuncDeclArg* ``,`` *FuncDeclArgsNonEmpty*

*FuncDeclArg* :math:`\rightarrow` *Identifier* ``:`` *TransientType*

*FuncDeclRet* :math:`\rightarrow` :math:`\epsilon`

*FuncDeclRet* :math:`\rightarrow` ``->`` *TransientType*

*StructDef* :math:`\rightarrow` ``struct`` *Identifier* ``{`` *StructDefBody* ``}``

*StructDefBody* :math:`\rightarrow` *VariableDefinition* *StructDefBody*

*StructDefBody* :math:`\rightarrow` :math:`\epsilon`

*Statement* :math:`\rightarrow` *CompoundStatement*

*Statement* :math:`\rightarrow` *Expression* ``;``

*Statement* :math:`\rightarrow` *VariableDefinition* ``;``

*Statement* :math:`\rightarrow` ``if`` ``(`` *Expression* ``)`` *Statement*

*Statement* :math:`\rightarrow` ``if`` ``(`` *Expression* ``)`` *Statement* ``else`` *Statement*

*Expression* :math:`\rightarrow` *CompoundExpression*

*Expression* :math:`\rightarrow` *Literal*

*Expression* :math:`\rightarrow` *Identifier*

*Expression* :math:`\rightarrow` *Expression* ``(`` *FuncCallArguments* ``)``

*Expression* :math:`\rightarrow` *Expression* **op** *Expression* [#Operations]_

*Expression* :math:`\rightarrow` *Expression* **op** [#Operations]_

*Expression* :math:`\rightarrow` **op** *Expression* [#Operations]_

*Expression* :math:`\rightarrow` **cast_type** ``!`` *TemplateParam* ``(`` *Expression* ``)``

*Expression* :math:`\rightarrow` *Type*

*Expression* :math:`\rightarrow` ``if`` ``(`` *Expression* ``)`` *CompoundExpression* ``else`` *CompoundExpression* [#ConditionalExpression]_

*TemplateParam* :math:`\rightarrow` **id**

*TemplateParam* :math:`\rightarrow` ``(`` *Expression* ``)``

*Literal* :math:`\rightarrow` *LiteralInt*

*Literal* :math:`\rightarrow` *LiteralString*

*Literal* :math:`\rightarrow` *LiteralFP*

*Literal* :math:`\rightarrow` *LiteralPointer*

*LiteralString* :math:`\rightarrow` **literal_string**

*LiteralInt* :math:`\rightarrow` **literal_int**

*LiteralFP* :math:`\rightarrow` **literal_fp**

*LiteralPointer* :math:`\rightarrow` ``null``

*CompoundStatement* :math:`\rightarrow` ``{`` *StatementList* ``}``

*CompoundExpression* :math:`\rightarrow` ``{`` *StatementList* *Expression* ``}``

*StatementList* :math:`\rightarrow` :math:`\epsilon`

*StatementList* :math:`\rightarrow` *StatementList* *Statement*

*TransientType* :math:`\rightarrow` *Type*

*TransientType* :math:`\rightarrow` *Type* ``ref``

*Type* :math:`\rightarrow` *Identifier*

*Type* :math:`\rightarrow` *Type* ``@``

*Type* :math:`\rightarrow` *Type* ``[`` LiteralInt ``]``

*VariableDefinition* :math:`\rightarrow` ``def`` *VariableDeclBody*

*VariableDefinition* :math:`\rightarrow` ``def`` *VariableDeclBody* ``=`` *Expression*

*VariableDeclBody* :math:`\rightarrow` *Identifier* ``:`` *Type*

*Identifier* :math:`\rightarrow` **identifier**

*FuncCallArguments* :math:`\rightarrow` :math:`\epsilon`

*FuncCallArguments* :math:`\rightarrow` *FuncCallArgumentsNonEmpty*

*FuncCallArgumentsNonEmpty* :math:`\rightarrow` *Expression*

*FuncCallArgumentsNonEmpty* :math:`\rightarrow` *Expression* ``,`` *FuncCallArgumentsNonEmpty*

.. rubric:: Footnotes

.. [#Operations] For list of actual operators and their precedence, see :doc:`operators`.
.. [#ConditionalExpression]
    A conditional expression *must* have an ``else`` clause, as it must return a value regardless of the condition's result.
