---
title: 如何：使用事务更新模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: e24436a5-7f97-401b-bc83-20d188d10d5b
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cd66c62d74bfe63d8376b5520b42cb20c8c0a3a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651611"
---
# <a name="how-to-use-transactions-to-update-the-model"></a>如何：使用事务更新模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

事务确保对存储区所做的更改被视为组。 可以将已分组的更改作为一个单元提交或回滚。

 每当程序代码修改、添加或删除可视化和建模 SDK 中的存储区中的任何元素时 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，它都必须在事务内执行此操作。 <xref:Microsoft.VisualStudio.Modeling.Transaction>发生更改时，必须有与存储关联的活动实例。 这适用于所有模型元素、关系、形状、关系图及其属性。

 事务机制可帮助避免不一致的状态。 如果在事务中发生错误，则回滚所有更改。 如果用户执行撤消命令，则每个最近的事务将被视为单个步骤。 用户不能撤消最近更改的某些部分，除非您将它们显式放置在单独的事务中。

## <a name="opening-a-transaction"></a>打开事务
 管理事务的最便捷方法是将 `using` 语句包含在 `try...catch` 语句中：

```
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

 如果在更改期间阻止最后发生的异常 `Commit()` ，则会将存储重置为其以前的状态。 这有助于确保错误不会使模型处于不一致状态。

 可以在一个事务内进行任意数量的更改。 您可以在活动事务内打开新事务。 嵌套事务必须在包含事务结束之前提交或回滚。 有关详细信息，请参阅属性的示例 <xref:Microsoft.VisualStudio.Modeling.Transaction.TransactionDepth%2A> 。

 若要使您的更改成为永久更改，您应该在 `Commit` 该事务被释放之前进行。 如果发生未在事务中捕获的异常，则会将存储重置为其在更改前的状态。

## <a name="rolling-back-a-transaction"></a>回滚事务
 若要确保存储在事务之前处于或还原到其状态，可以使用以下两种策略之一：

1. 引发未在事务范围内捕获的异常。

2. 显式回滚事务：

    ```
    this.Store.TransactionManager.CurrentTransaction.Rollback();
    ```

## <a name="transactions-do-not-affect-non-store-objects"></a>事务不影响非存储对象
 事务仅控制存储的状态。 它们不能撤消对外部项（如文件、数据库或在 DSL 定义之外用普通类型声明的对象）进行的部分更改。

 如果异常可能会导致此类更改与存储不一致，则应在异常处理程序中处理这种可能性。 确保外部资源与存储对象保持同步的一种方法是使用事件处理程序将每个外部对象耦合到存储区元素。 有关详细信息，请参阅 [事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

## <a name="rules-fire-at-the-end-of-a-transaction"></a>在事务结束时触发规则
 在事务结束时，在释放事务之前，将触发附加到存储区中的元素的规则。 每个规则都是应用于已更改模型元素的方法。 例如，有 "修复" 规则，该规则在其模型元素发生更改时更新形状的状态，以及在创建模型元素时创建形状。 没有指定的触发顺序。 规则所做的更改可能会激发另一个规则。

 您可以定义自己的规则。 有关规则的详细信息，请参阅 [响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

 规则不会在撤消、重做或回滚命令后激发。

## <a name="transaction-context"></a>事务上下文
 每个事务都有一个字典，你可以在其中存储所需的任何信息：

 `store.TransactionManager`

 `.CurrentTransaction.TopLevelTransaction`

 `.Context.Add(aKey, aValue);`

 这对于在规则之间传输信息特别有用。

## <a name="transaction-state"></a>事务状态
 在某些情况下，如果更改是通过撤消或重做事务引起的，则需要避免传播更改。 例如，如果你编写可更新存储中其他值的属性值处理程序，则可能会发生这种情况。 由于撤消操作会将存储中的所有值重置为先前的状态，因此不需要计算更新的值。 使用以下代码：

```
if (!this.Store.InUndoRedoOrRollback) {...}
```

 最初从文件加载存储时，可能会触发规则。 若要避免响应这些更改，请使用：

```
if (!this.Store.InSerializationTransaction) {...}

```
