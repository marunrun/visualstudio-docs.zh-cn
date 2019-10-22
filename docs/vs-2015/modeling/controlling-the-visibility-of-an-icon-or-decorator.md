---
title: 控制图标或修饰器的可见性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 2697fd5d-b936-4b6b-b87b-be64825dc7a4
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 49cecff999e0155209ba58c20c0d623b15d63698
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667832"
---
# <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>控制图标或修饰器的可见性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*修饰*器是在特定于域的语言（DSL）的形状上显示的图标或文本行。 您可以根据模型中属性的状态，使修饰器出现和消失。 例如，在代表人员的形状上，可能会根据人员的性别、子女数等显示不同的图标。

## <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>控制图标或修饰器的可见性
 下面的过程假定您已经定义了一个形状及其到域类的映射。 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。

#### <a name="to-control-the-visibility-of-an-icon-or-text-decorator"></a>控制图标或文本修饰器的可见性

1. 在 DSL 定义关系图中，向 shape 类添加要显示的图标或文本修饰器。

   1. 右键单击该形状类，指向 "**添加**"，然后单击所需的修饰器类型。

   2. 设置修饰器的**位置**属性。 多个修饰器可以具有相同的位置。 例如，你可以将 "男" 和 "女性" 图标共享同一位置。

   3. 设置图标修饰器的**默认图标**属性。

2. 选择 "关系图元素映射"，这是 DSL 定义关系图上的形状类和域类之间的灰色线条。

3. 在 "DSL 详细信息" 窗口的 "**修饰器映射**" 选项卡中，选择一个修饰器。 例如，MaleDecorator。

4. 检查 "**可见性筛选器**" 框。

5. 如果应控制可见性的域属性位于直属域类上，请将 "**筛选路径" 属性**留空。

    否则，单击下拉菜单，并导航到属性所在的关系或类。

   - 若要避免出现错误报告，则不应在导航工具中浏览标记为 "*" 的关系。

6. 将 "**筛选器" 属性**设置为域属性。 例如，性别。

7. 在 "**可见性项**" 列表中，添加应显示其修饰器的此域属性的值。 例如，男性。

8. 对于每个图标，请重复上述步骤。

9. **转换所有模板**，生成并运行，并打开测试关系图。

10. 更改控制属性值时，修饰器应会出现并消失。

    通常，您希望使用比简单的值集更复杂的公式来控制可见性。 例如，若要使图标依赖于特定类型的链接数，或要使其依赖于某个数字是否在特定范围内。 在这种情况下，请使用以下过程。

#### <a name="to-control-the-visibility-of-a-decorator-based-on-a-formula"></a>基于公式控制修饰器的可见性

1. 向域类添加计算域属性。 在 "**属性**" 窗口中，设置以下值：

     **IsBrowsable =** `False` **-这将隐藏用户的属性**

     **Kind =** `Calculated` **-这意味着你将提供用于计算其值的代码**

     例如**DecoratorControl**的**名称**

     **类型** =  `Boolean`

     有关详细信息，请参阅[计算的和自定义的存储属性](../modeling/calculated-and-custom-storage-properties.md)。

2. 使新属性控制修饰器的可见性。

    1. 选择 "关系图元素映射"，它是从域类到形状的灰色线条。 在 " **DSL 详细信息**" 窗口中，打开 " **DecoratorMap** " 选项卡。

    2. 检查 "**可见性筛选器**" 框。

    3. 在 "**筛选器" 属性**中，选择控件属性 " **DecoratorControl**"。

    4. 在 "**可见性项**" 下，输入 `True`。

3. 单击 "解决方案资源管理器" 工具栏中的 "**转换所有模板**"。

4. 单击 "**生成**" 菜单上的 "**生成解决方案**"。

5. 双击出现的错误报告： "*YourClass*不包含 GetDecoratorControlValue 的定义 ..."。

     文本编辑器将在 Dsl\GeneratedCode\DomainClasses.cs. 上打开。 上面突出显示的错误是要求添加方法的注释。

6. 请注意缺少的命名空间、类和方法。  例如，FamilyTree. GetDecoratorControlValue （）。

7. 在单独的代码文件中，编写包含缺少的方法的分部类定义。 例如:

    ```
    namespace Company.FamilyTree
    { partial class Person
      { bool GetDecoratorControlValue()
        {
          return this.Children.Count > 0;
    } } }
    ```

     有关使用程序代码自定义模型的详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

8. 重新生成并运行解决方案。

## <a name="see-also"></a>请参阅
 [定义形状和连接线](../modeling/defining-shapes-and-connectors.md)在[关系图上设置背景图像](../modeling/setting-a-background-image-on-a-diagram.md)[在程序代码中导航和更新模型在](../modeling/navigating-and-updating-a-model-in-program-code.md)[编写代码以定制域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
