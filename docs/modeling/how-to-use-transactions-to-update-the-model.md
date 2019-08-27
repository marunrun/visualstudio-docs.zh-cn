---
title: 如何：使用事务更新模型
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9a7514e3ff0c876a669f514a7e17bb02b73c19c2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936844"
---
# <a name="how-to-use-transactions-to-update-the-model"></a>如何：使用事务更新模型
事务，请确保对在存储区所做的更改被视为一个组。 可以提交或回滚作为一个单元进行分组的更改。

 每次您的程序代码修改、 添加，或删除 Visual Studio 可视化和建模 SDK 中的存储区中的任何元素，它必须在事务内执行。 必须有应用的活动实例<xref:Microsoft.VisualStudio.Modeling.Transaction>更改发生时与应用商店相关联。 这适用于所有模型元素、 关系、 形状、 图和它们的属性。

 事务机制可帮助您避免不一致的状态。 如果在事务期间发生错误，将回滚所有更改。 如果用户执行的撤消命令时，每个新的事务被视为单步执行。 除非显式将其放在单独的事务，则用户不能撤消的最新更改的部分。

## <a name="opening-a-transaction"></a>打开一个事务
 管理事务的最简便的方法是使用`using`语句括在`try...catch`语句：

```csharp
Store store; ...
try
{
  using (Transaction transaction =
    store.TransactionManager.BeginTransaction("update model"))
    // Outermost transaction must always have a name.
  {
    // Make several changes in Store:
    Person p = new Person(store);
    p.FamilyTreeModel = familyTree;
    p.Name = "Edward VI";
    // end of changes to Store

    transaction.Commit(); // Don't forget this!
  } // transaction disposed here
}
catch (Exception ex)
{
  // If an exception occurs, the Store will be
  // rolled back to its previous state.
}
```

 如果异常，则最后`Commit()`过程中发生更改，在存储区将重置为其以前的状态。 这可帮助你确保错误不会为不一致状态中保留该模型。

 可以任意数量的一个事务内的更改。 您可以打开在活动事务内部的新事务。 嵌套的事务必须提交或回滚包含事务结束之前。 有关详细信息，请参阅示例<xref:Microsoft.VisualStudio.Modeling.Transaction.TransactionDepth%2A>属性。

 若要永久所做的更改，您应`Commit`之前被释放的事务。 如果发生在事务内未捕获到异常，存储将重置为其状态之前所做的更改。

## <a name="rolling-back-a-transaction"></a>回滚事务
 若要确保在存储区将保留在或将恢复到事务执行前的状态，可以使用这些策略之一：

1. 引发未捕获事务的作用域内的异常。

2. 回滚显式事务：

    ```csharp
    this.Store.TransactionManager.CurrentTransaction.Rollback();
    ```

## <a name="transactions-do-not-affect-non-store-objects"></a>事务不会影响非存储对象
 事务仅控制与存储的状态。 它们不能撤消对外部的项，如文件、 数据库或已使用外部 DSL 定义的普通类型声明的对象所做的部分更改。

 如果异常可能会使此类更改与应用商店不一致，您应处理的异常处理程序中的这种可能性。 请确保外部资源保持与存储区对象同步的一种方法是使用事件处理程序耦合到存储区中元素的每个外部对象。 有关详细信息，请参阅[事件处理程序传播更改外部模型](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

## <a name="rules-fire-at-the-end-of-a-transaction"></a>事务结束时的规则触发
 在事务结束时，释放事务之前，会触发附加到存储区中的元素的规则。 每个规则都应用于已更改的模型元素的方法。 例如，有"修复"的规则，更新形状的状态时其模型元素已更改，并创建模型元素时，其创建形状。 没有任何指定的激发顺序。 由规则所做的更改可以触发另一个规则。

 可以定义自己的规则。 有关规则的详细信息，请参阅[对的响应并传播更改](../modeling/responding-to-and-propagating-changes.md)。

 规则不会撤消、 重做或回滚命令之后激发。

## <a name="transaction-context"></a>事务上下文
 每个事务都有一个字典，可以在其中存储所需的任何信息：

 `store.TransactionManager`

 `.CurrentTransaction.TopLevelTransaction`

 `.Context.Add(aKey, aValue);`

 这是特别有用的规则之间传输信息。

## <a name="transaction-state"></a>事务状态
 在某些情况下，需要避免传播更改，如果更改由正在撤消或重做事务。 这可能发生，例如，如果您编写的属性值处理程序可以更新存储区中的另一个值。 撤消操作将存储区中的所有值重都置为以前的状态，因为它不需要计算更新后的值。 使用以下代码：

```csharp
if (!this.Store.InUndoRedoOrRollback) {...}
```

 在存储区最初从文件加载时，可以触发规则。 若要避免对这些更改作出响应，请使用：

```csharp
if (!this.Store.InSerializationTransaction) {...}
```