---
title: 控制图标或修饰器的可见性
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7cfe6ce02b03ed69435f8056ccd340b92f9eb5a4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62421494"
---
# <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>控制图标或修饰器的可见性
一个*修饰器*为图标或特定于域的语言 (DSL) 中的一个形状显示的文本行。 可以进行修饰器出现，并根据模型中的属性的状态会消失。 例如上表示一个人的形状，, 可能有不同的图标显示具体取决于该人员的性别，子项，数等等。

## <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>控制图标或修饰器的可见性
 以下过程假设已定义形状和其映射到域类。 有关详细信息，请参阅[如何定义特定于域的语言](../modeling/how-to-define-a-domain-specific-language.md)。

#### <a name="to-control-the-visibility-of-an-icon-or-text-decorator"></a>若要控制图标或文本的修饰器的可见性

1. 在 DSL 定义关系图中，图标或你想要显示的文本修饰器添加到形状类。

   1. 右键单击形状类、 指向**添加**，然后单击所需的类型的修饰器。

   2. 设置修饰器的**位置**属性。 多个修饰器可以具有相同的位置。 例如，你可以为 male 和 female 共享相同的位置的图标。

   3. 设置**默认图标**图标修饰器的属性。

2. 选择关系图元素映射，这是形状类和 DSL 定义关系图上的域类之间的灰色线条。

3. 在 DSL 详细信息窗口中**修饰器映射**选项卡上，选择修饰器。 例如，MaleDecorator。

4. 检查**可见性筛选器**框。

5. 如果应控制可见性的域属性是即时的域类上，将保留**筛选器属性的路径**保留为空。

    否则为单击下拉列表菜单，然后导航到关系或类属性所在的位置。

   - 若要避免错误报告，您应导航通过关系标记为"*"导航工具中。

6. 设置**筛选器属性**为域属性。 例如，性别。

7. 在中**可见性条目**列表中，添加为其修饰器应显示此域属性的值。 例如，男性。

8. 重复的每个图标的步骤。

9. **转换所有模板**、 生成和运行和打开测试关系图。

10. 更改控制的属性值时，修饰器应出现并消失。

    通常情况下，你想要查看由一组简单的值比更为复杂的公式来控制。 例如，若要将具有依赖于特定类型的链接数图标，或以使其取决于是否的号码标识特定范围内。 在这种情况下，使用以下过程。

#### <a name="to-control-the-visibility-of-a-decorator-based-on-a-formula"></a>若要控制修饰器根据公式的可见性

1. 将计算的域属性添加到域类。 在中**属性**窗口中，设置以下值：

     **IsBrowsable =**`False`**-这将隐藏来自用户的属性**

     **类型 =**`Calculated`**-这意味着您将在提供计算其值的代码**

     **名称**例如**DecoratorControl**

     **Type** = `Boolean`

     有关详细信息，请参阅[计算和自定义存储属性](../modeling/calculated-and-custom-storage-properties.md)。

2. 请控制修饰器的可见性的新属性。

    1. 选择关系图元素映射，它是从域类到形状中的灰色线。 在中**DSL 详细信息**窗口中，打开**DecoratorMap**选项卡。

    2. 检查**可见性筛选器**框。

    3. 在中**筛选器属性**，选择的控件属性**DecoratorControl**。

    4. 下**可见性条目**，输入`True`。

3. 单击**转换所有模板**中**解决方案资源管理器**工具栏。

4. 单击**生成解决方案**上**生成**菜单。

5. 双击错误报告，其中显示："*YourClass*不包含定义为 GetDecoratorControlValue..."。

     在 Dsl\GeneratedCode\DomainClasses.cs 上打开文本编辑器。 上面突出显示的错误是请求你添加的方法的注释。

6. 请注意缺少的命名空间、 类和方法。  例如，Company.FamilyTree.Person.GetDecoratorControlValue()。

7. 在单独的代码文件中编写分部类定义包含缺少的方法。 例如：

    ```
    namespace Company.FamilyTree
    { partial class Person
      { bool GetDecoratorControlValue()
        {
          return this.Children.Count > 0;
    } } }
    ```

     有关自定义使用程序代码模型的详细信息，请参阅[导航和更新程序代码中的模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

8. 重新生成并运行解决方案。

## <a name="see-also"></a>请参阅

- [定义形状和连接线](../modeling/defining-shapes-and-connectors.md)
- [在图表上设置背景图像](../modeling/setting-a-background-image-on-a-diagram.md)
- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)