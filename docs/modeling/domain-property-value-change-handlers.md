---
title: 域属性值更改处理程序
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, overriding event handlers
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 46bf3d8a188899e27e7a83d875cf970583858ba8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653781"
---
# <a name="domain-property-value-change-handlers"></a>域属性值更改处理程序

在 Visual Studio 域特定语言中，当域属性的值发生更改时，将在域属性处理程序中调用 `OnValueChanging()` 和 `OnValueChanged()` 方法。 若要响应更改，可以重写这些方法。

## <a name="override-the-property-handler-methods"></a>重写属性处理程序方法

域特定语言的每个域属性都由嵌入在其父域类内的类处理。 其名称遵循格式*PropertyName*PropertyHandler。 可以在文件**Dsl\Generated Code\DomainClasses.cs**中检查此属性处理程序类。 在该类中，在值发生更改前立即调用 `OnValueChanging()`，在值发生更改后立即调用 `OnValueChanged()`。

例如，假设你有一个名为 `Comment` 的域类，其中包含名为 `Text` 的字符串域属性和一个名为 `TextLengthCount` 的整数属性。 若要导致 `TextLengthCount` 始终包含 `Text` 字符串的长度，可在 Dsl 项目的单独文件中编写以下代码：

```csharp
// Domain Class "Comment":
public partial class Comment
{
  // Domain Property "Text":
  partial class TextPropertyHandler
  {
    protected override void OnValueChanging(CommentBase element, string oldValue, string newValue)
    {
      base.OnValueChanging(element, oldValue, newValue);

      // To update values outside the Store, write code here.

      // Let the transaction manager handle undo:
      Store store = element.Store;
      if (store.InUndoRedoOrRollback || store.InSerializationTransaction) return;

      // Update values in the Store:
      this.TextLengthCount = newValue.Length;
    }
  }
}
```

请注意关于属性处理程序的以下几点：

- 在满足以下两个条件时调用属性处理程序方法：用户对域属性做出更改以及程序代码将不同的值分配给该属性。

- 仅在该值实际发生更改时才调用这些方法。 如果程序代码分配的值等于当前值，则不调用该处理程序。

- 计算属性和自定义存储域属性不具有 OnValueChanged 和 OnValueChanging 方法。

- 无法使用更改处理程序来修改新值。 如果想要执行此操作（例如，若要将该值限制在特定范围内），请定义 `ChangeRule`。

- 无法将更改处理程序添加到表示关系的角色的属性。 相反，可在关系类上定义 `AddRule` 和 `DeleteRule`。 当创建或更改链接时，将触发这些规则。 有关详细信息，请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

### <a name="changes-in-and-out-of-the-store"></a>存储内外的更改

属性处理程序方法将在已启动更改的事务内部进行调用。 因此，你可以在存储内进行更多更改，而无需打开新事务。 所做的更改可能会导致其他处理程序调用。

当事务处于正在撤消、重做或回滚状态时，不应在存储中进行更改，即对模型元素、关系、形状、连接符、关系图或其属性进行更改。

此外，通常不应在从文件加载该模型时更新值。

因此，对模型所做的更改应通过测试进行保护，如下所示：

```csharp
if (!store.InUndoRedoOrRollback && !store. InSerializationTransaction)
{
   this.TextLength = ...; // in-store changes
}
```

相反，如果属性处理程序在存储外传播更改（例如，对文件、数据库或非存储变量的更改），则应始终进行这些更改，以便在用户调用撤消或重做时更新外部值。

### <a name="cancel-a-change"></a>取消更改

如果想要阻止更改，可以回滚当前事务。 例如，你可能想要确保属性保持在特定范围内。

```csharp
if (newValue > 10)
{
   store.TransactionManager.CurrentTransaction.Rollback();
   System.Windows.Forms.MessageBox.Show("Value must be less than 10");
}
```

### <a name="alternative-technique-calculated-properties"></a>替代技术：计算属性

上一示例显示了如何使用 OnValueChanged() 来将值从一个域属性传播到另一个域属性。 每个属性都具有其自己的存储值。

相反，你可以考虑将派生属性定义为计算属性。 在这种情况下，该属性不具有其自己的存储，并且将定义每当需要其值时要计算的函数。 有关详细信息，请参阅[计算的和自定义的存储属性](../modeling/calculated-and-custom-storage-properties.md)。

除了前面的示例，你还可以将 `TextLengthCount` 的**Kind**字段设置为在 DSL 定义中进行**计算**。 您可以为此域属性提供自己的**Get**方法。 **Get**方法将返回 `Text` 字符串的当前长度。

但是，计算属性的一个潜在缺点是每当使用该值时都要计算表达式，这可能会出现性能问题。 此外，计算属性上不存在 OnValueChanging() 和 OnValueChanged()。

### <a name="alternative-technique-change-rules"></a>替代技术：更改规则

如果定义 ChangeRule，则在事务结束时，将在属性的值发生更改的情况下执行它。  有关详细信息，请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

如果在一个事务中进行了多项更改，则在完成全部更改后才能执行 ChangeRule。 与此相反，OnValue如果尚未执行某些更改，则会执行方法。 根据你想要实现的目的，这可能使 ChangeRule 变得更合适。

还可以使用 ChangeRule 调整属性的新值，使其保持在特定范围内。

> [!WARNING]
> 如果一条规则对存储内容进行了更改，则可能会触发其他规则和属性处理程序。 如果一条规则更改了触发它的属性，则它将被再次调用。 必须确保规则定义不会导致无限触发。

```csharp
using Microsoft.VisualStudio.Modeling;
...
// Change rule on the domain class Comment:
[RuleOn(typeof(Comment), FireTime = TimeToFire.TopLevelCommit)]
class MyCommentTrimRule : ChangeRule
{
  public override void
    ElementPropertyChanged(ElementPropertyChangedEventArgs e)
  {
    base.ElementPropertyChanged(e);
    Comment comment = e.ModelElement as Comment;

    if (comment.Text.StartsWith(" ") || comment.Text.EndsWith(" "))
      comment.Text = comment.Text.Trim();
    // If changed, rule will trigger again.
  }
}

// Register the rule:
public partial class MyDomainModel
{
 protected override Type[] GetCustomDomainModelTypes()
 { return new Type[] { typeof(MyCommentTrimRule) };
 }
}
```

## <a name="example"></a>示例

### <a name="description"></a>描述

以下示例将重写域属性的属性处理程序，并在 `ExampleElement` 域类的属性已发生更改时通知用户。

### <a name="code"></a>代码

```csharp
using DslModeling = global::Microsoft.VisualStudio.Modeling;
using DslDesign = global::Microsoft.VisualStudio.Modeling.Design;

namespace msft.FieldChangeSample
{
  public partial class ExampleElement
  {
    internal sealed partial class NamePropertyHandler
    {
      protected override void OnValueChanged(ExampleElement element,
         string oldValue, string newValue)
      {
        if (!this.Store.InUndoRedoOrRollback)
        {
           // make in-store changes here...
        }
        // This part is called even in undo:
        System.Windows.Forms.MessageBox.Show("Value Has Changed");
        base.OnValueChanged(element, oldValue, newValue);
      }
    }
  }
}
```