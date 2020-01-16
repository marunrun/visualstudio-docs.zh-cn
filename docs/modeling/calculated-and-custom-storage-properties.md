---
title: 计算的和自定义的存储属性
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain properties
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 52915f0bac2bd172daf909541ecfa86396d90a5d
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76115196"
---
# <a name="calculated-and-custom-storage-properties"></a>计算的和自定义的存储属性
域特定语言（DSL）中的所有域属性都可以在关系图和语言浏览器中显示给用户，并可通过程序代码进行访问。 但是，属性的值存储方式有所不同。

## <a name="kinds-of-domain-properties"></a>域属性的种类
 在 DSL 定义中，可以设置域属性的**类型**，如下表所示：

|域属性类型|描述|
|-|-|
|**标准**（默认值）|保存在*存储区*中并序列化为文件的域属性。|
|**所得**|只读域属性，该属性不保存在存储区中，而是从其他值计算而来的。<br /><br /> 例如，可以从 `Person.BirthDate`计算 `Person.Age`。<br /><br /> 您必须提供执行计算的代码。 通常，您需要计算其他域属性的值。 不过，您也可以使用外部资源。|
|**自定义存储**|不会直接保存在存储区中，而是可以获取和设置的域属性。<br /><br /> 您必须提供获取和设置值的方法。<br /><br /> 例如，可以将 `Person.FullAddress` 存储在 `Person.StreetAddress`、`Person.City`和 `Person.PostalCode`中。<br /><br /> 您还可以访问外部资源，例如从数据库中获取和设置值。<br /><br /> 如果 `Store.InUndoRedoOrRollback` 为 true，则代码不应在存储中设置值。 请参阅[事务和自定义资源库](#setters)。|

## <a name="providing-the-code-for-a-calculated-or-custom-storage-property"></a>为计算的或自定义的存储属性提供代码
 如果将域属性的种类设置为 "计算" 或 "自定义存储"，则必须提供访问方法。 生成解决方案时，错误报告会告诉您需要什么。

#### <a name="to-define-a-calculated-or-custom-storage-property"></a>定义计算或自定义的存储属性

1. 在 Dsldefinition.dsl 中，在关系图中或在**Dsl 资源管理器**中选择域属性。

2. 在 "**属性**" 窗口中，将 "**类型**" 字段设置为**计算** **存储或自定义存储**。

     确保还将其类型设置为所需的**类型**。

3. 单击 "**解决方案资源管理器**的工具栏中的"**转换所有模板**"。

4. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

     收到以下错误消息： "*YourClass*不包含 Get*yourproperty '* 的定义"。

5. 双击错误消息。

     此时将打开 Dsl\GeneratedCode\DomainClasses.cs 或 DomainRelationships.cs。 在突出显示的方法调用的上方，注释会提示你提供 Get*yourproperty '* （）的实现。

    > [!NOTE]
    > 此文件是从 Dsldefinition.dsl 生成的。 如果编辑此文件，则下次单击 "**转换所有模板**" 时，所做的更改将丢失。 相反，请在单独的文件中添加所需的方法。

6. 在单独的文件夹中创建或打开一个类文件，例如 CustomCode\\*YourDomainClass*。

     确保命名空间与生成的代码中的命名空间相同。

7. 在类文件中，编写域类的部分实现。 在类中，为缺少的 `Get` 方法编写一个类似于以下示例的定义：

    ```
    namespace Company.FamilyTree
    {  public partial class Person
       {  int GetAgeValue()
          { return System.DateTime.Today.Year - this.BirthYear; }
    }  }
    ```

8. 如果将**种类**设置为 "**自定义存储**"，则还必须提供 `Set` 方法。 例如：

    ```
    void SetAgeValue(int value)
    { if (!Store.InUndoRedoOrRollback)
        this.BirthYear =
            System.DateTime.Today.Year - value; }
    ```

     如果 `Store.InUndoRedoOrRollback` 为 true，则代码不应在存储中设置值。 请参阅[事务和自定义资源库](#setters)。

9. 生成和运行解决方案。

10. 测试属性。 请确保尝试 "**撤消**" 和 "**重做**"。

## <a name="setters"></a>事务和自定义资源库
 在 "自定义存储" 属性的 "设置" 方法中，无需打开事务，因为通常在活动事务内调用方法。

 但是，如果用户调用撤消或重做操作，或者如果正在回滚事务，则也可以调用 Set 方法。 如果 <xref:Microsoft.VisualStudio.Modeling.Store.InUndoRedoOrRollback%2A> 为 true，则设置方法应如下所示：

- 它不应在存储中进行更改，例如向其他域属性分配值。 撤消管理器将设置其值。

- 但是，它应该更新任何外部资源（如数据库或文件内容）或存储区之外的对象。 这将确保它们与存储区中的值保持 synchronism。

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

 有关事务的详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

## <a name="see-also"></a>另请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [域属性的属性](../modeling/properties-of-domain-properties.md)
- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
