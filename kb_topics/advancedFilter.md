# Advanced Filtering

[← Back to API Index](../reference.md)

---

## KB Topic: Advanced Filtering

### Description
Isomorphic [DataSources](../classes/DataSource.md#class-datasource) provide an advanced filtering mechanism for searching data, including a wide range of builtin [search-operators](../reference_2.md#object-operator), which allow searching via simple comparisons like `equals` and `contains` and more complex checks, like `equalsOtherField` and `regex`. You can also add entirely custom search-operators, via DataSource method [addSearchOperator()](../classes/DataSource.md#method-datasourceaddsearchoperator).

For a full list of operators, see [OperatorId](../reference.md#type-operatorid).

### Related

- [OperatorValueType](../reference.md#type-operatorvaluetype)
- [OperatorId](../reference.md#type-operatorid)
- [DataSource.addSearchOperator](../classes/DataSource.md#classmethod-datasourceaddsearchoperator)
- [DataSource.setTypeOperators](../classes/DataSource.md#classmethod-datasourcesettypeoperators)
- [Operator.condition](../classes/Operator.md#method-operatorcondition)
- [Operator.compareCriteria](../classes/Operator.md#method-operatorcomparecriteria)
- [DataSource.addSearchOperator](../classes/DataSource.md#method-datasourceaddsearchoperator)
- [DataSource.getSearchOperator](../classes/DataSource.md#method-datasourcegetsearchoperator)
- [DataSource.getTypeOperators](../classes/DataSource.md#method-datasourcegettypeoperators)
- [DataSource.setTypeOperators](../classes/DataSource.md#method-datasourcesettypeoperators)
- [DataSource.getFieldOperators](../classes/DataSource.md#method-datasourcegetfieldoperators)
- [DataSource.getFieldDefaultOperator](../classes/DataSource.md#method-datasourcegetfielddefaultoperator)
- [DataSource.getFieldOperatorMap](../classes/DataSource.md#method-datasourcegetfieldoperatormap)
- [DataSource.getTypeOperatorMap](../classes/DataSource.md#method-datasourcegettypeoperatormap)
- [DataSource.evaluateCriterion](../classes/DataSource.md#method-datasourceevaluatecriterion)
- [AdvancedCriteria](../reference.md#object-advancedcriteria)
- [Criterion](../reference.md#object-criterion)
- [Operator](../reference_2.md#object-operator)
- [AdvancedCriteria.strictSQLFiltering](../reference.md#attr-advancedcriteriastrictsqlfiltering)
- [Criterion.operator](../classes/Criterion.md#attr-criterionoperator)
- [Criterion.fieldName](../classes/Criterion.md#attr-criterionfieldname)
- [Criterion.value](../classes/Criterion.md#attr-criterionvalue)
- [Criterion.criteria](../classes/Criterion.md#attr-criterioncriteria)
- [Criterion.start](../classes/Criterion.md#attr-criterionstart)
- [Criterion.end](../classes/Criterion.md#attr-criterionend)
- [Operator.ID](../classes/Operator.md#attr-operatorid)
- [Operator.title](../classes/Operator.md#attr-operatortitle)
- [Operator.titleProperty](../classes/Operator.md#attr-operatortitleproperty)
- [Operator.textTitle](../classes/Operator.md#attr-operatortexttitle)
- [Operator.textTitleProperty](../classes/Operator.md#attr-operatortexttitleproperty)
- [Operator.fieldTypes](../classes/Operator.md#attr-operatorfieldtypes)
- [Operator.requiresServer](../classes/Operator.md#attr-operatorrequiresserver)
- [Operator.hidden](../classes/Operator.md#attr-operatorhidden)
- [Operator.valueType](../classes/Operator.md#attr-operatorvaluetype)
- [Operator.usageHint](../classes/Operator.md#attr-operatorusagehint)
- [Operator.editorType](../classes/Operator.md#attr-operatoreditortype)
- [Operator.symbol](../classes/Operator.md#attr-operatorsymbol)
- [DataSourceField.validOperators](../classes/DataSourceField.md#attr-datasourcefieldvalidoperators)
- [DataSourceField.defaultOperator](../classes/DataSourceField.md#attr-datasourcefielddefaultoperator)
- [DynamicForm.allowExpressions](../classes/DynamicForm.md#attr-dynamicformallowexpressions)
- [FormItem.allowExpressions](../classes/FormItem.md#attr-formitemallowexpressions)
- [FormItem.validOperators](../classes/FormItem.md#attr-formitemvalidoperators)
- [FormItem.defaultOperator](../classes/FormItem.md#attr-formitemdefaultoperator)
- [SimpleType.validOperators](../classes/SimpleType.md#attr-simpletypevalidoperators)
- [SimpleType.defaultOperator](../classes/SimpleType.md#attr-simpletypedefaultoperator)
- [ListGridField.allowFilterExpressions](../classes/ListGridField.md#attr-listgridfieldallowfilterexpressions)
- [ListGrid.allowFilterExpressions](../classes/ListGrid_1.md#attr-listgridallowfilterexpressions)

---
