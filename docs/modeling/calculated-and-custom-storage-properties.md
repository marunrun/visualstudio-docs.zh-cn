---
title: 计算的和自定义的存储属性
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain properties
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1ca2401333f7678b821b5c6fa68f7953a91996d0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440024"
---
# <a name="calculated-and-custom-storage-properties"></a>计算的和自定义的存储属性
域特定语言 (DSL) 中的所有域属性可以显示给用户在关系图上和在语言资源管理器中，并且可以通过程序代码访问。 但是，属性不同的方式存储它们的值。

## <a name="kinds-of-domain-properties"></a>类型的域属性
 在 DSL 定义中，你可以将**种类**域属性，如以下表中列出的：

|域的属性类型|描述|
|-|-|
|**标准**（默认值）|保存在一个域属性*存储*和序列化到文件。|
|**计算**|一个只读的域属性，则不保存在存储中，但是计算从其他值。<br /><br /> 例如，`Person.Age`无法从计算`Person.BirthDate`。<br /><br /> 您必须提供执行计算的代码。 通常情况下，您可以计算从其他域属性的值。 但是，您还可以使用外部资源。|
|**自定义存储**|域属性，直接在存储中，不保存，但可以是 get 和 set。<br /><br /> 您必须提供用于获取和设置值的方法。<br /><br /> 例如，`Person.FullAddress`可能存储在`Person.StreetAddress`， `Person.City`，和`Person.PostalCode`。<br /><br /> 此外可以访问外部资源，例如若要获取和设置从数据库的值。<br /><br /> 你的代码不应在存储中设置值时`Store.InUndoRedoOrRollback`为 true。 请参阅[事务和自定义资源库](#setters)。|

## <a name="providing-the-code-for-a-calculated-or-custom-storage-property"></a>为计算或自定义存储属性提供的代码
 如果您设置域属性的类型为 Calculated 或自定义存储，你必须提供访问方法。 生成解决方案时，错误报告将告诉您的要求。

#### <a name="to-define-a-calculated-or-custom-storage-property"></a>若要定义的计算或自定义存储属性

1. 在 DslDefinition.dsl 中，选择域属性在关系图中或在**DSL 资源管理器**。

2. 在中**属性**窗口中，将**种类**字段**计算**或**自定义存储**。

     请确保还设置其**类型**到所需的内容。

3. 单击**转换所有模板**中的工具栏**解决方案资源管理器**。

4. 在 **“生成”** 菜单上，单击 **“生成解决方案”**。

     收到以下错误消息："*YourClass*不包含定义 get*YourProperty*。"

5. 双击该错误消息。

     在 Dsl\GeneratedCode\DomainClasses.cs 或 DomainRelationships.cs 将打开。 上面突出显示的方法调用中，注释会提示你提供一个实现 get*YourProperty*（)。

    > [!NOTE]
    > 从 DslDefinition.dsl 生成此文件。 如果编辑此文件时，所做的更改将会丢失您单击下一次**转换所有模板**。 相反，在单独的文件添加所需的方法。

6. 创建或打开类文件在单独的文件夹，例如独特\\*YourDomainClass*。 cs。

     请确保该命名空间是生成的代码相同。

7. 在类文件中，编写域类的部分实现。 在类中，编写缺少的定义`Get`方法类似于下面的示例：

    ```
    namespace Company.FamilyTree
    {  public partial class Person
       {  int GetAgeValue()
          { return System.DateTime.Today.Year - this.BirthYear; }
    }  }
    ```

8. 如果您设置**种类**到**自定义存储**，你将需要提供`Set`方法。 例如：

    ```
    void SetAgeValue(int value)
    { if (!Store.InUndoRedoOrRollback)
        this.BirthYear =
            System.DateTime.Today.Year - value; }
    ```

     你的代码不应在存储中设置值时`Store.InUndoRedoOrRollback`为 true。 请参阅[事务和自定义资源库](#setters)。

9. 生成和运行解决方案。

10. 测试属性。 请确保您尝试**撤消**并**重做**。

## <a name="setters"></a> 事务和自定义资源库
 在自定义存储属性的 Set 方法，您无需打开事务，因为通常在活动事务内部调用的方法。

 但是，如果用户调用撤消或重做操作，或者如果正在回滚事务可能还调用 Set 方法。 当<xref:Microsoft.VisualStudio.Modeling.Store.InUndoRedoOrRollback%2A>为 true，Set 方法的行为，如下所示：

- 它不应在存储中，例如将值分配给其他域属性进行更改。 撤消管理器将设置其值。

- 但是，它应更新任何外部资源，例如数据库或文件的内容或存储外的对象。 这将确保，它们保存在 synchronism 存储区中的值。

  例如：

```
void SetAgeValue(int value)
{
  // If we are in Undo, no changes to Store objects:
  if (!this.Store.InUndoRedoOrRollback)
  {
    this.BirthYear = System.DateTime.Today.Year - value;
  }
  // But always update external objects:
  System.IO.File.WriteAllText(AgeFile, value);
}
```

 有关事务的详细信息，请参阅[导航和更新程序代码中的模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

## <a name="see-also"></a>请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [域属性的属性](../modeling/properties-of-domain-properties.md)
- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)