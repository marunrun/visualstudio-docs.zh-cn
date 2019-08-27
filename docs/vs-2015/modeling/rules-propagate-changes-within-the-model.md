---
title: 规则在模型内部传播更改 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, rules
ms.assetid: 1690a38a-c8f5-4bc6-aab9-015771ec6647
caps.latest.revision: 32
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 29950be152c140a8315f96f8752b1fa906c3f801
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442932"
---
# <a name="rules-propagate-changes-within-the-model"></a>规则在模型内部传播更改
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以创建将更改传播从一个元素到另一个可视化和建模 SDK (VMSDK) 中的存储规则。 在存储区中的任何元素更改时，规则计划执行，通常在最外部事务提交时。 有不同类型的规则对于不同类型的事件，如添加一个元素，或删除它。 可以将规则附加到特定类型的元素、 形状或关系图。 许多内置功能由规则定义： 例如，规则可确保在模型更改时，更新关系图。 可以添加自己的规则来自定义您的特定于域的语言。  

 传播更改内部应用商店 – 也就是说，更改到模型元素、 关系、 形状或连接符和其域属性，应用商店规则是特别有用。 当用户调用撤消或重做命令不会运行规则。 相反，事务管理器可确保存储内容被还原到正确的状态。 如果你想要将更改传播到应用商店以外的资源，使用存储事件。 有关详细信息，请参阅[事件处理程序传播更改外部模型](../modeling/event-handlers-propagate-changes-outside-the-model.md)。  

 例如，假设你想要指定只要用户 （或你的代码） 创建新的元素的类型 ExampleDomainClass，另一种类型的其他元素在另一个模型的一部分进行创建。 无法编写 AddRule，并将其与 ExampleDomainClass 关联。 您应在规则创建的其他元素中编写代码。  

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

    // Code here propagates change as required – for example:  
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
> 规则的代码应更改仅的商店; 内的元素的状态也就是说，该规则应更改仅模型元素、 关系、 形状、 连接器、 关系图或它们的属性。 如果你想要将更改传播到应用商店以外的资源，定义存储事件。 有关详细信息，请参阅[事件处理程序传播更改外部模型](../modeling/event-handlers-propagate-changes-outside-the-model.md)  

### <a name="to-define-a-rule"></a>若要定义规则  

1. 定义规则，如类前缀为`RuleOn`属性。 该属性将规则与其中一个域类、 关系或关系图元素相关联。 规则将应用于此类，这可能是抽象的每个实例。  

2. 通过将其添加到返回的集注册规则`GetCustomDomainModelTypes()`域模型类中。  

3. 规则类派生的一个抽象的规则类，并编写的代码执行方法。  

   以下部分介绍这些步骤的更多详细信息。  

### <a name="to-define-a-rule-on-a-domain-class"></a>域类上定义规则  

- 自定义代码文件中定义的类和它前面加<xref:Microsoft.VisualStudio.Modeling.RuleOnAttribute>属性：  

    ```  
    [RuleOn(typeof(ExampleElement),   
         // Usual value – but required, because it is not the default:  
         FireTime = TimeToFire.TopLevelCommit)]   
    class MyRule ...  

    ```  

- 中的第一个参数的使用者类型可以是域类、 域关系、 形状、 连接符或关系图。 通常情况下，将规则应用于域类和关系。  

     `FireTime`通常是`TopLevelCommit`。 这可确保仅进行的事务的所有主要更改后执行规则。 备选方法是内联的这在更改; 后立即执行该规则和 LocalCommit，规则的当前事务 （这可能不是最外面） 结束时执行。 此外可以设置会影响在队列中，其排序顺序的规则的优先级，但这是一个不可靠的方法的实现所需的结果。  

- 作为使用者类型，可以指定一个抽象类。  

- 此规则适用于所有使用者类的实例。  

- 默认值为`FireTime`是 TimeToFire.TopLevelCommit。 这会导致最外部事务提交时要执行的规则。 一种替代方法是 TimeToFire.Inline。 这将导致触发事件后立即执行的规则。  

### <a name="to-register-the-rule"></a>若要注册规则  

- 将规则类添加到的返回类型列表`GetCustomDomainModelTypes`域模型中：  

    ```  
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

- 如果您不确定域模型类的名称，该文件中查找**Dsl\GeneratedCode\DomainModel.cs**  

- 在 DSL 项目中的自定义代码文件中编写此代码。  

### <a name="to-write-the-code-of-the-rule"></a>若要编写规则的代码  

- 从以下基类之一派生规则类：  

  |                             基类                              |                                                                                                                                                                                                                                                                                                                                                                              触发器                                                                                                                                                                                                                                                                                                                                                                              |
  |---------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  |           <xref:Microsoft.VisualStudio.Modeling.AddRule>            |                                                                                                                                                                                                                                                                                                                        添加元素、 链接或形状。<br /><br /> 用于检测新关系，除了新元素。                                                                                                                                                                                                                                                                                                                        |
  |          <xref:Microsoft.VisualStudio.Modeling.ChangeRule>          | 更改域属性值。 该方法的参数提供的旧的和新值。<br /><br /> 对于形状，触发此规则时内置`AbsoluteBounds`属性更改，如果移动形状。<br /><br /> 在许多情况下，它是更方便地重写`OnValueChanged`或`OnValueChanging`属性处理程序中。 更改立即之前和之后调用这些方法。 与此相反，该规则通常在事务结束时运行。 有关详细信息，请参阅[域属性值更改处理程序](../modeling/domain-property-value-change-handlers.md)。 **注意：** 创建或删除链接时，则不会触发此规则。 相反，编写`AddRule`和一个`DeleteRule`域关系。 |
  |         <xref:Microsoft.VisualStudio.Modeling.DeletingRule>         |                                                                                                                                                                                                                                                                                                             当某个元素或链接是即将被删除时触发。 该属性 ModelElement.IsDeleting 事务结束时才为 true。                                                                                                                                                                                                                                                                                                              |
  |          <xref:Microsoft.VisualStudio.Modeling.DeleteRule>          |                                                                                                                                                                                                       已删除的元素或链接时执行。 已执行的所有其他规则，包括 DeletingRules 后执行规则。 ModelElement.IsDeleting 为 false，并且 ModelElement.IsDeleted 为 true。 若要允许后续撤销，该元素并不实际删除从内存中，但从 Store.ElementDirectory 中删除。                                                                                                                                                                                                       |
  |           <xref:Microsoft.VisualStudio.Modeling.MoveRule>           |                                                                                                                                                                                                                                                                                                           元素是从一个存储分区移动到另一个。<br /><br /> （请注意这不相关的图形形状的位置。）                                                                                                                                                                                                                                                                                                            |
  |     <xref:Microsoft.VisualStudio.Modeling.RolePlayerChangeRule>     |                                                                                                                                                                                                                                                                                                                 此规则仅适用于域关系。 如果显式将模型元素分配给链接的任一端，它会触发。                                                                                                                                                                                                                                                                                                                 |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerPositionChangeRule> |                                                                                                                                                                                                                                                                                                                   链接到或从元素的顺序在链接上使用 MoveBefore 或 MoveToIndex 方法发生更改时触发。                                                                                                                                                                                                                                                                                                                    |
  |   <xref:Microsoft.VisualStudio.Modeling.TransactionBeginningRule>   |                                                                                                                                                                                                                                                                                                                                                              创建一个事务时执行。                                                                                                                                                                                                                                                                                                                                                              |
  |  <xref:Microsoft.VisualStudio.Modeling.TransactionCommittingRule>   |                                                                                                                                                                                                                                                                                                                                                      执行事务时，将为已提交。                                                                                                                                                                                                                                                                                                                                                      |
  |  <xref:Microsoft.VisualStudio.Modeling.TransactionRollingBackRule>  |                                                                                                                                                                                                                                                                                                                                                     要回滚事务时执行。                                                                                                                                                                                                                                                                                                                                                     |

- 每个类有一个方法重写。 类型`override`来发现它在类中。 此方法的参数标识要更改的元素。  

  请注意有关规则的以下几点：  

1. 组在事务中的更改可能会触发许多规则。 通常情况下，当最外面的事务提交时，会执行规则。 中未指定的顺序执行它们。  

2. 始终在事务内执行规则。 因此，无需创建一个新事务来进行更改。  

3. 事务回滚时，或执行撤消或重做操作时，不会执行规则。 这些操作将在存储区中的所有内容重都置为其以前的状态。 因此，如果你的规则发生更改的应用商店之外的任何内容的状态，它可能保留在与应用商店 synchronism 内容。 若要更新在存储外的状态，则最好使用事件。 有关详细信息，请参阅[事件处理程序传播更改外部模型](../modeling/event-handlers-propagate-changes-outside-the-model.md)。  

4. 从文件加载模型时，将执行一些规则。 若要确定是否加载或保存正在进行，请使用`store.TransactionManager.CurrentTransaction.IsSerializing`。  

5. 如果你的规则的代码创建更多规则触发器，它们将添加到激发列表的末尾，并在事务完成之前将执行。 DeletedRules 筛选器之后执行的所有其他规则。 一个规则可以在事务中，每个更改一次运行多次。  

6. 要传递到和从规则的信息，您可以将信息存储在`TransactionContext`。 这是仅在事务期间维护的字典。 在事务结束时，它已被释放。 每个规则中的事件自变量提供对它的访问。 请记住规则未按可预测的顺序执行。  

7. 在考虑其他备选方法后使用规则。 例如，如果你想要更新属性值发生更改时，请考虑使用计算的属性。 如果你想要约束的大小或形状的位置，使用`BoundsRule`。 如果你想要对属性值的更改作出响应，将添加`OnValueChanged`给属性的处理程序。 有关详细信息，请参阅[对的响应并传播更改](../modeling/responding-to-and-propagating-changes.md)。  

## <a name="example"></a>示例  
 域关系实例化，若要链接两个元素时，下面的示例将更新一个属性。 不仅用户创建一个链接上一个关系图，而且还如果程序代码将创建一个链接时，将会触发规则。  

 若要测试此示例中，创建 DSL 使用任务流解决方案模板，并在 Dsl 项目中的文件中插入以下代码。 生成和运行解决方案，并在调试项目中打开示例文件。 注释形状和数据流元素之间绘制注释链接。 在注释中的文本更改为已连接到的最新元素上的报表。  

 在实践中，通常会为每个 AddRule 编写 DeleteRule。  

```  
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
 [事件处理程序模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)   
 [BoundsRules 约束形状位置和大小](../modeling/boundsrules-constrain-shape-location-and-size.md)
