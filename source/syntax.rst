******
Syntax
******

Grammar
=======

*Module* :math:`\rightarrow` *GlobalExpressionsList*

*GlobalExpressionsList* :math:`\rightarrow` :math:`\epsilon`

*GlobalExpressionList* :math:`\rightarrow` *GlobalExpressionList* *GlobalExpression*

*GlobalExpression* :math:`\rightarrow` *FuncDef*

*FuncDef* :math:`\rightarrow` ``def`` *FuncDeclBody* *Statement*

*FuncDef* :math:`\rightarrow` ``def`` *FuncDeclBody* *Expression*

*FuncDeclBody* :math:`\rightarrow` *Identifier* ``(`` *FuncDeclArgs* ``)`` *FuncDeclRet*

*FuncDeclArgs* :math:`\rightarrow` :math:`\epsilon`

*FuncDeclArgs* :math:`\rightarrow` *FuncDeclArgsNonEmpty*

*FuncDeclArgsNonEmpty* :math:`\rightarrow` *FuncDeclArg*

*FuncDeclArgsNonEmpty* :math:`\rightarrow` *FuncDeclArg* ``,`` *FuncDeclArgsNonEmpty*

*FuncDeclArg* :math:`\rightarrow` *Identifier* ``:`` *Type*

*FuncDeclRet* :math:`\rightarrow` :math:`\epsilon`

*FuncDeclRet* :math:`\rightarrow` ``->`` *Type*

*Statement* :math:`\rightarrow` *CompoundStatement*

*Statement* :math:`\rightarrow` *Expression* ``;``

*Statement* :math:`\rightarrow` *VariableDefinition* ``;``

*Statement* :math:`\rightarrow` ``if`` ``(`` *Expression* ``)`` *Statement*

*Statement* :math:`\rightarrow` ``if`` ``(`` *Expression* ``)`` *Statement* ``else`` *Statement*

*Expression* :math:`\rightarrow` *CompoundExpression*

*Expression* :math:`\rightarrow` *Literal*

*Expression* :math:`\rightarrow` *Identifier*

*Expression* :math:`\rightarrow` *Expression* ``(`` *FuncCallArguments* ``)``

*Expression* :math:`\rightarrow` *Expression* **op** *Expression* [#operations]_

*Expression* :math:`\rightarrow` *Expression* **op**

*Expression* :math:`\rightarrow` **op** *Expression*

*Expression* :math:`\rightarrow` **cast_type** ``!`` *TemplateParam* ``(`` *Expression* ``)``

*Expression* :math:`\rightarrow` *Type*

*Expression* :math:`\rightarrow` ``if`` ``(`` *Expression* ``)`` *CompoundExpression* ``else`` *CompoundExpression*

*TemplateParam* :math:`\rightarrow` **id**

*TemplateParam* :math:`\rightarrow` ``(`` *Expression* ``)``

*Literal* :math:`\rightarrow` **literal_string**

*Literal* :math:`\rightarrow` **literal_int**

*Literal* :math:`\rightarrow` **literal_fp**

*CompoundStatement* :math:`\rightarrow` ``{`` *StatementList* ``}``

*CompoundExpression* :math:`\rightarrow` ``{`` *StatementList* *Expression* ``}``

*StatementList* :math:`\rightarrow` :math:`\epsilon`

*StatementList* :math:`\rightarrow` *StatementList* *Statement*

*Type* :math:`\rightarrow` *Identifier*

*VariableDefinition* :math:`\rightarrow` ``def`` *VariableDeclBody*

*VariableDefinition* :math:`\rightarrow` ``def`` *VariableDeclBody* ``=`` *Expression*

*VariableDeclBody* :math:`\rightarrow` *Identifier* ``:`` *Type*

*Identifier* :math:`\rightarrow` **identifier**

*FuncCallArguments* :math:`\rightarrow` :math:`\epsilon`

*FuncCallArguments* :math:`\rightarrow` *FuncCallArgumentsNonEmpty*

*FuncCallArgumentsNonEmpty* :math:`\rightarrow` *Expression*

*FuncCallArgumentsNonEmpty* :math:`\rightarrow` *Expression* ``,`` *FuncCallArgumentsNonEmpty*

.. rubric:: Footnotes

.. [#operations] For list of actual operators and their precedence, see https://github.com/Practical/practical-sa/wiki/Operators.
