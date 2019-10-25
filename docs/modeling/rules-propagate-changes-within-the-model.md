---
title: 规则在模型内部传播更改
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, rules
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 74d64b4fe0c0aa5293e11daad13f632c4a487736
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747421"
---
# <a name="rules-propagate-changes-within-the-model"></a>规则在模型内部传播更改
你可以创建一个存储规则，以便在可视化和建模 SDK （VMSDK）中将更改从一个元素传播到另一个元素。 当存储区中的任何元素发生更改时，将计划执行规则，通常是在最外面的事务提交时执行。 不同类型的事件有不同类型的规则，例如添加元素或删除元素。 您可以将规则附加到特定类型的元素、形状或关系图。 许多内置功能都是由规则定义的：例如，规则确保在模型更改时更新关系图。 可以通过添加自己的规则来自定义域特定语言。

 应用商店规则特别适用于在存储区中传播更改，即对模型元素、关系、形状或连接符及其域属性的更改。 当用户调用 "撤消" 或 "重做" 命令时，规则不会运行。 相反，事务管理器会确保将存储内容还原到正确的状态。 如果要将更改传播到存储区之外的资源，请使用存储事件。 有关详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

 例如，假设你想要指定每当用户（或你的代码）创建 ExampleDomainClass 类型的新元素时，也会在模型的另一部分中创建另一个类型的其他元素。 可以编写 AddRule 并将其与 ExampleDomainClass 相关联。 您可以在规则中编写代码来创建其他元素。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;

namespace ExampleNamespace
{
 // Attribute associates the rule with a domain class:
 [RuleOn(typeof(ExampleDomainClass), FireTime=TimeToFire.TopLevelCommit)]
 // The rule is a class derived from one of the abstract rules:
 class MyAddRule : AddRule
 {
  // Override the abstract method:
  public override void ElementAdded(ElementAddedEventArgs e)
  {
    base.ElementAdded(e);
    ExampleDomainClass element = e.ModelElement;
    Store store = element.Store;
    // Ignore this call if we're currently loading a model:
    if (store.TransactionManager.CurrentTransaction.IsSerializing)
       return;

    // Code here propagates change as required - for example:
      AnotherDomainClass echo = new AnotherDomainClass(element.Partition);
      echo.Name = element.Name;
      echo.Parent = element.Parent;
    }
  }
 // The rule must be registered:
 public partial class ExampleDomainModel
 {
   protected override Type[] GetCustomDomainModelTypes()
   {
     List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
     types.Add(typeof(MyAddRule));
     // If you add more rules, list them here.
     return types.ToArray();
   }
 }
}
```

> [!NOTE]
> 规则的代码只应更改存储区中元素的状态;也就是说，规则只应更改模型元素、关系、形状、连接符、关系图或其属性。 如果要将更改传播到存储区之外的资源，请定义存储事件。 有关详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

### <a name="to-define-a-rule"></a>定义规则

1. 将规则定义为带有 `RuleOn` 特性前缀的类。 该属性将规则与某个域类、关系或关系图元素相关联。 该规则将应用于此类的每个实例，这可能是抽象的。

2. 注册规则，方法是将其添加到域模型类中 `GetCustomDomainModelTypes()` 返回的集中。

3. 从一个抽象规则类派生规则类，并编写执行方法的代码。

   以下部分更详细地介绍了这些步骤。

### <a name="to-define-a-rule-on-a-domain-class"></a>在域类上定义规则

- 在自定义代码文件中，定义一个类并在其前面加上 <xref:Microsoft.VisualStudio.Modeling.RuleOnAttribute> 特性：

    ```csharp
    [RuleOn(typeof(ExampleElement),
         // Usual value - but required, because it is not the default:
         FireTime = TimeToFire.TopLevelCommit)]
    class MyRule ...

    ```

- 第一个参数中的使用者类型可以是域类、域关系、形状、连接符或关系图。 通常，将规则应用于域类和关系。

     @No__t_0 通常 `TopLevelCommit`。 这可确保仅在事务的所有主要更改完成后才执行规则。 替代项为内联，这会在更改后立即执行规则;和 LocalCommit，它在当前事务（可能不是最外面的）结束时执行规则。 你还可以设置规则的优先级，以影响其在队列中的顺序，但这是实现所需结果的不可靠方法。

- 您可以指定一个抽象类作为使用者类型。

- 此规则适用于 subject 类的所有实例。

- @No__t_0 的默认值为 TimeToFire. TopLevelCommit。 这会导致在最外面的事务提交时执行规则。 替代项为 TimeToFire。 这将导致规则在触发事件之后立即执行。

### <a name="to-register-the-rule"></a>注册规则

- 将规则类添加到域模型中 `GetCustomDomainModelTypes` 返回的类型列表中：

    ```csharp
    public partial class ExampleDomainModel
     {
       protected override Type[] GetCustomDomainModelTypes()
       {
         List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
         types.Add(typeof(MyAddRule));
         // If you add more rules, list them here.
         return types.ToArray();
       }
     }

    ```

- 如果你不确定域模型类的名称，请在文件**Dsl\GeneratedCode\DomainModel.cs**中查看。

- 在 DSL 项目的自定义代码文件中编写此代码。

### <a name="to-write-the-code-of-the-rule"></a>编写规则代码

- 从下面的一个基类派生规则类：

  | 基类 | 触发器 |
  |-|-|
  | <xref:Microsoft.VisualStudio.Modeling.AddRule> | 添加了元素、链接或形状。<br /><br /> 除了新元素外，还可以使用此项检测新的关系。 |
  | <xref:Microsoft.VisualStudio.Modeling.ChangeRule> | 域属性值已更改。 方法参数提供旧值和新值。<br /><br /> 对于形状，如果移动了某个内置 `AbsoluteBounds` 属性，则会触发此规则。<br /><br /> 在许多情况下，更方便地在属性处理程序中重写 `OnValueChanged` 或 `OnValueChanging`。 这些方法将在更改前后立即调用。 与此相反，规则通常在事务结束时运行。 有关详细信息，请参阅[域属性值更改处理程序](../modeling/domain-property-value-change-handlers.md)。 **注意：** 当创建或删除链接时，不会触发此规则。 请改为写入域关系的 `AddRule` 和 `DeleteRule`。 |
  | <xref:Microsoft.VisualStudio.Modeling.DeletingRule> | 要删除元素或链接时触发。 在事务结束之前，属性 ModelElement IsDeleting 为 true。 |
  | <xref:Microsoft.VisualStudio.Modeling.DeleteRule> | 删除元素或链接时执行。 规则在执行所有其他规则后执行，包括 DeletingRules。 ModelElement. IsDeleting 为 false，而 ModelElement 为 true。 若要允许后续撤消，元素实际上不会从内存中删除，而是从 ElementDirectory 中删除。 |
  | <xref:Microsoft.VisualStudio.Modeling.MoveRule> | 元素从一个存储区分区移到另一个存储区。<br /><br /> （请注意，这与形状的图形位置无关。） |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerChangeRule> | 此规则仅适用于域关系。 如果将模型元素显式分配到链接的任意一端，则会触发此方法。 |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerPositionChangeRule> | 当使用链接上的 MoveBefore 或 MoveToIndex 方法更改了元素的链接顺序或从元素进行的更改时触发。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionBeginningRule> | 在创建事务时执行。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionCommittingRule> | 要提交事务时执行。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionRollingBackRule> | 当事务即将回滚时执行。 |

- 每个类都有一个重写的方法。 在类中键入 `override`，以发现它。 此方法的参数标识要更改的元素。

  请注意以下有关规则的要点：

1. 事务中的更改集可能会触发多个规则。 通常情况下，在最外面的事务提交时执行规则。 它们按未指定的顺序执行。

2. 规则始终在事务内部执行。 因此，您无需创建新事务即可进行更改。

3. 当回滚事务或执行撤消或重做操作时，不会执行规则。 这些操作将存储的所有内容重置为其以前的状态。 因此，如果规则更改了存储外部的任何内容的状态，它可能不会与存储内容保持 synchronism。 若要更新存储外部的状态，最好使用事件。 有关详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

4. 从文件加载模型时，会执行某些规则。 若要确定加载或保存是否正在进行，请使用 `store.TransactionManager.CurrentTransaction.IsSerializing`。

5. 如果规则的代码创建更多规则触发器，它们将被添加到触发列表的末尾，并在事务完成之前执行。 DeletedRules 在所有其他规则之后执行。 一个规则可在一个事务中运行多次，每次更改一次。

6. 若要向/从规则传递信息，你可以将信息存储在 `TransactionContext` 中。 这只是在事务中维护的字典。 当事务结束时，将释放它。 每个规则中的事件参数都提供对它的访问。 请记住，规则不按可预测顺序执行。

7. 考虑其他替代项后使用规则。 例如，如果想要在值更改时更新属性，请考虑使用计算属性。 如果要限制形状的大小或位置，请使用 `BoundsRule`。 如果要响应属性值的更改，请将 `OnValueChanged` 处理程序添加到属性。 有关详细信息，请参阅[响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

## <a name="example"></a>示例
 下面的示例在将域关系实例化为链接两个元素时更新属性。 仅当用户在关系图上创建了一个链接，并且程序代码创建了一个链接时，才会触发此规则。

 若要测试此示例，请使用 "任务流" 解决方案模板创建 DSL，并在 Dsl 项目的文件中插入以下代码。 生成并运行解决方案，然后在调试项目中打开示例文件。 在注释形状和 flow 元素之间绘制注释链接。 注释中的文本将更改为报表已连接到的最近元素。

 在实践中，通常会为每个 AddRule 编写一个 DeleteRule。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualStudio.Modeling;

namespace Company.TaskRuleExample
{

  [RuleOn(typeof(CommentReferencesSubjects))]
  public class RoleRule : AddRule
  {

    public override void ElementAdded(ElementAddedEventArgs e)
    {
      base.ElementAdded(e);
      CommentReferencesSubjects link = e.ModelElement as CommentReferencesSubjects;
      Comment comment = link.Comment;
      FlowElement subject = link.Subject;
      Transaction current = link.Store.TransactionManager.CurrentTransaction;
      // Don't want to run when we're just loading from file:
      if (current.IsSerializing) return;
      comment.Text = "Flow has " + subject.FlowTo.Count + " outgoing connections";
    }

  }

  public partial class TaskRuleExampleDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(RoleRule));
      return types.ToArray();
    }
  }

}
```

## <a name="see-also"></a>请参阅

- [事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)