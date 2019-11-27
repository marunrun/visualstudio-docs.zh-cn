---
title: 自定义元素创建和移动 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.elementmergedirective
helpviewer_keywords:
- Domain-Specific Language, element merge directives
ms.assetid: cbd28f15-dfd7-46bd-ab79-5430e3ed83c8
caps.latest.revision: 38
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8189330f5bc3ff5c9008b6f01ffc00af96162806
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301152"
---
# <a name="customizing-element-creation-and-movement"></a>自定义元素创建和移动
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过工具箱或粘贴或移动操作，允许将元素拖至另一个元素上。 您可以使用您指定的关系将移动的元素链接到目标元素。

 元素合并指令（EMD）指定将一个模型元素*合并*到另一个模型元素时会发生的情况。 发生这种情况的原因有：

- 用户将 "工具箱" 拖动到关系图或形状上。

- 用户使用资源管理器或隔离舱形状中的 "添加" 菜单创建元素。

- 用户将项从一个泳道移到另一个泳道。

- 用户粘贴元素。

- 程序代码将调用元素合并指令。

  尽管创建操作似乎不同于复制操作，但它们实际上是以相同的方式工作的。 添加元素（例如，从 "工具箱"）时，将复制该元素的原型。 原型以与从模型的另一部分复制的元素相同的方式合并到模型中。

  EMD 的责任是决定如何将对象或对象组合并到模型中的特定位置。 具体而言，它会确定应实例化哪些关系以将合并组链接到模型。 您还可以对其进行自定义以设置属性和创建其他对象。

  ![DSL&#45;EMD&#95;合并](../modeling/media/dsl-emd-merge.png "DSL-EMD_Merge")元素合并指令的角色

  当您定义嵌入关系时，将自动生成 EMD。 当用户将新的子实例添加到父级时，此默认 EMD 将创建关系的实例。 可以通过添加自定义代码来修改这些默认 EMDs。

  你还可以在 DSL 定义中添加自己的 EMDs，以允许用户拖动或粘贴合并类和接收类的不同组合。

## <a name="defining-an-element-merge-directive"></a>定义元素合并指令
 您可以向域类、域关系、形状、连接符和关系图添加元素合并指令。 可以在 "接收域" 类下的 "DSL 资源管理器" 中添加或查找它们。 接收类是已在模型中的元素的域类，新的或复制的元素将合并到该类中。

 ![DSL&#45;EMD&#95;详细信息](../modeling/media/dsl-emd-details.png "DSL-EMD_Details")

 **索引类**是可合并到接收类的成员中的元素的域类。 索引类的子类的实例还将通过此 EMD 合并，除非您将应用于**子类**设置为 False。

 有两种类型的 merge 指令：

- **进程合并**指令指定应将新元素链接到树中的关系。

- **正向合并**指令将新元素重定向到另一个接收元素，通常是父级。

  您可以将自定义代码添加到合并指令：

- Set**使用自定义接受**添加您自己的代码，以确定是否应将索引元素的特定实例合并到目标元素。 当用户从 "工具箱" 拖动时，如果代码不允许合并，则会显示 "无效" 指针。

   例如，您可以仅在接收元素处于特定状态时允许合并。

- Set**使用自定义合并**来添加自己的代码，以定义执行合并时对模型所做的更改。

   例如，您可以使用模型中的数据从其新位置设置合并元素中的属性。

> [!NOTE]
> 如果你编写自定义合并代码，它只会影响使用此 EMD 执行的合并。 如果有其他 EMDs 合并相同类型的对象，或者存在其他在不使用 EMD 的情况下创建这些对象的自定义代码，则它们将不会受到自定义合并代码的影响。
>
> 如果要确保新元素或新关系始终由您的自定义代码进行处理，请考虑在嵌入关系上定义 `AddRule`，并对元素的域类定义 `DeleteRule`。 有关详细信息，请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

## <a name="example-defining-an-emd-without-custom-code"></a>示例：定义不含自定义代码的 EMD
 下面的示例通过从 "工具箱" 拖到现有形状上，使用户能够同时创建一个元素和一个连接器。 该示例将 EMD 添加到 DSL 定义。 在进行此修改之前，用户可以将工具拖动到关系图上，而不是拖到现有形状上。

 用户还可以将元素粘贴到其他元素上。

#### <a name="to-let-users-create-an-element-and-a-connector-at-the-same-time"></a>允许用户同时创建一个元素和一个连接器

1. 使用**最小语言**解决方案模板创建新的 DSL。

    当你运行此 DSL 时，它允许你在形状之间创建形状和连接线。 不能将新的**ExampleElement**形状从工具箱拖到现有形状上。

2. 若要允许用户将元素合并到 `ExampleElement` 形状上，请在 `ExampleElement` 域类中创建新的 EMD：

   1. 在**DSL 资源管理器**中，展开 "**域类**"。 右键单击 `ExampleElement`，然后单击 "**添加新元素合并指令**"。

   2. 确保 " **DSL 详细信息**" 窗口处于打开状态，以便您可以查看新 EMD 的详细信息。 （菜单： **View**、**其他窗口**、 **DSL 详细信息**。）

3. 在 "DSL 详细信息" 窗口中设置**索引类**，以定义可在 `ExampleElement` 对象上合并的元素类。

    对于本示例，请选择 "`ExampleElements`"，以便用户可以将新元素拖动到现有元素上。

    请注意，索引类将成为 DSL 资源管理器中的 EMD 的名称。

4. 在 "**通过创建链接进行处理合并**" 下，添加两个路径：

   1. 一个路径将新元素链接到父模型。 需要输入的路径表达式将从现有元素导航到父模型的嵌入关系。 最后，在新链接中指定将向其分配新元素的角色。 路径如下：

       `ExampleModelHasElements.ExampleModel/!ExampleModel/.Elements`

   2. 其他路径将新元素链接到现有元素。 路径表达式指定要向其分配新元素的引用关系和角色。 此路径如下所示：

       `ExampleElementReferencesTargets.Sources`

      可以使用路径导航工具创建每个路径：

   3. 在 "**处理合并" （通过在路径中创建链接**），单击 **\<添加路径 >** 。

   4. 单击列表项右侧的下拉箭头。 此时将显示一个树视图。

   5. 展开树中的节点，以形成要指定的路径。

5. 测试 DSL：

   1. 按 F5 重新生成并运行解决方案。

        重新生成的时间比平时长，因为生成的代码将从文本模板中更新以符合新的 DSL 定义。

   2. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例启动后，打开 DSL 的模型文件。 创建一些示例元素。

   3. 从**示例元素**工具拖到现有形状上。

        此时将显示一个新形状，并将其链接到使用连接符的现有形状。

   4. 复制现有形状。 选择另一个形状并粘贴。

        将创建第一个形状的副本。  它有一个新名称，并使用连接器链接到第二个形状。

   请注意此过程中的以下几点：

- 通过创建元素合并指令，可以允许任何类元素接受任何其他类。 EMD 是在接收域类中创建的，并且在 "**索引类**" 字段中指定了接受的域类。

- 通过定义路径，可以指定应使用哪些链接将新元素连接到现有模型。

     指定的链接应包含一个嵌入关系。

- EMD 会影响 "工具箱" 和 "粘贴" 操作的两项创建。

     如果编写用于创建新元素的自定义代码，则可以使用 `ElementOperations.Merge` 方法显式调用 EMD。 这将确保你的代码以与其他操作相同的方式将新元素链接到模型。 有关详细信息，请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。

## <a name="example-adding-custom-accept-code-to-an-emd"></a>示例：将自定义接受代码添加到 EMD
 通过将自定义代码添加到 EMD，可以定义更复杂的合并行为。 此简单示例防止用户向关系图中添加超出固定数目的元素。 该示例修改嵌入关系中附带的默认 EMD。

#### <a name="to-write-custom-accept-code-to-restrict-what-the-user-can-add"></a>编写自定义接受代码以限制用户可以添加的内容

1. 使用**最小语言**解决方案模板创建 DSL。 打开 DSL 定义关系图。

2. 在 DSL 资源管理器中，展开 "**域类**"、`ExampleModel`"**元素合并指令**"。 选择名为 `ExampleElement`的元素合并指令。

     此 EMD 控制用户如何在模型中创建新的 `ExampleElement` 对象，例如通过从工具箱中拖动。

3. 在 " **DSL 详细信息**" 窗口中，选择 "**使用自定义接受**"。

4. 重新生成解决方案。 这将花费比平时更长的时间，因为生成的代码将从模型中更新。

     将报告生成错误，如下所示： "ElementMergeSample. ExampleElement 不包含 CanMergeExampleElement 的定义 ..."

     必须实现 `CanMergeExampleElement`方法。

5. 在**Dsl**项目中创建新的代码文件。 将其内容替换为以下代码，并将命名空间更改为项目的命名空间。

    ```csharp
    using Microsoft.VisualStudio.Modeling;

    namespace Company.ElementMergeSample // EDIT.
    {
      partial class ExampleModel
      {
        /// <summary>
        /// Called whenever an ExampleElement is to be merged into this ExampleModel.
        /// This happens when the user pastes an ExampleElement
        /// or drags from the toolbox.
        /// Determines whether the merge is allowed.
        /// </summary>
        /// <param name="rootElement">The root element in the merging EGP.</param>
        /// <param name="elementGroupPrototype">The EGP that the user wants to merge.</param>
        /// <returns>True if the merge is allowed</returns>
        private bool CanMergeExampleElement(ProtoElementBase rootElement, ElementGroupPrototype elementGroupPrototype)
        {
          // Allow no more than 4 elements to be added:
          return this.Elements.Count < 4;
        }
      }
    }

    ```

     这个简单的示例限制了可合并到父模型中的元素数。 对于更有趣的条件，该方法可以检查接收对象的任何属性和链接。 它还可以检查在 <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype>中携带的合并元素的属性。 有关 `ElementGroupPrototypes`的详细信息，请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。 有关如何编写读取模型的代码的详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

6. 测试 DSL：

    1. 按 F5 重新生成解决方案。 当 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例打开时，打开 DSL 的实例。

    2. 通过几种方式创建新元素：

        1. 从**示例元素**工具拖到关系图上。

        2. 在**示例模型资源管理器**中，右键单击根节点，然后单击 "**添加新示例元素**"。

        3. 复制并粘贴关系图上的元素。

    3. 验证不能使用这些方法中的任何一种向模型添加四个以上的元素。 这是因为它们都使用元素合并指令。

## <a name="example-adding-custom-merge-code-to-an-emd"></a>示例：向 EMD 添加自定义合并代码
 在 "自定义合并代码" 中，可以定义当用户拖动某个工具或将其粘贴到某个元素上时会发生的情况。 可以通过两种方法定义自定义合并：

1. 集**使用自定义合并**并提供所需的代码。 你的代码将替换生成的合并代码。 如果要完全重新定义合并的功能，请使用此选项。

2. 重写 `MergeRelate` 方法，并选择性地重写 `MergeDisconnect` 方法。 为此，必须设置域类的 "**生成双派生**" 属性。 你的代码可以调用基类中生成的合并代码。 如果希望在执行合并后执行其他操作，请使用此选项。

   这些方法只影响使用此 EMD 执行的合并。 如果要影响可创建合并元素的所有方法，另一种方法是在嵌入关系上定义 `AddRule`，并对合并域类定义 `DeleteRule`。 有关详细信息，请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

#### <a name="to-override-mergerelate"></a>重写 MergeRelate

1. 在 DSL 定义中，确保定义了要向其添加代码的 EMD。 如果需要，可以添加路径并定义自定义接受代码，如前一部分中所述。

2. 在 Dsldefinition.dsl 关系图中，选择合并的接收类。 通常，它是嵌入关系的源端的类。

     例如，在从最小语言解决方案生成的 DSL 中，选择 `ExampleModel`。

3. 在 "**属性**" 窗口中，设置生成派生为 True 的**双精度** **值**。

4. 重新生成解决方案。

5. 检查**Dsl\Generated Files\DomainClasses.cs**的内容。 搜索名为 `MergeRelate` 的方法，并检查其内容。 这将帮助你编写自己的版本。

6. 在新的代码文件中，为接收类写入一个分部类，并重写 `MergeRelate` 方法。 请记住调用基方法。 例如:

    ```csharp
    partial class ExampleModel
    {
      /// <summary>
      /// Called when the user drags or pastes an ExampleElement onto the diagram.
      /// Sets the time of day as the name.
      /// </summary>
      /// <param name="sourceElement">Element to be added</param>
      /// <param name="elementGroup">Elements to be merged</param>
      protected override void MergeRelate(ModelElement sourceElement, ElementGroup elementGroup)
      {
        // Connect the element according to the EMD:
        base.MergeRelate(sourceElement, elementGroup);

        // Custom actions:
        ExampleElement mergingElement = sourceElement as ExampleElement;
        if (mergingElement != null)
        {
          mergingElement.Name = DateTime.Now.ToLongTimeString();
        }
      }
    }

    ```

#### <a name="to-write-custom-merge-code"></a>编写自定义合并代码

1. 在**Dsl\Generated Code\DomainClasses.cs**中，检查名为 `MergeRelate`的方法。 这些方法在新元素和现有模型之间创建链接。

    同时，检查名为 `MergeDisconnect`的方法。 当删除元素时，这些方法会将其从模型中取消链接。

2. 在 " **DSL 资源管理器**" 中，选择或创建要自定义的元素合并指令。 在 " **DSL 详细信息**" 窗口中，设置 "**使用自定义合并**"。

    如果设置此选项，则将忽略 "**处理合并**" 和 "**前向合并**" 选项。 改为使用您的代码。

3. 重新生成解决方案。 这将花费比平时更长的时间，因为生成的代码文件将从模型中更新。

    将显示错误消息。 双击错误消息以查看生成的代码中的说明。 这些说明要求提供两种方法，`MergeRelate`*YourDomainClass*和 `MergeDisconnect`*YourDomainClass*

4. 在单独的代码文件中编写分部类定义中的方法。 之前检查的示例应该建议所需的内容。

   自定义合并代码不会影响直接创建对象和关系的代码，也不会影响其他 EMDs。 若要确保无论如何创建元素都实现其他更改，请考虑改为写入 `AddRule` 和 `DeleteRule`。 有关详细信息，请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

## <a name="redirecting-a-merge-operation"></a>重定向合并操作
 正向合并指令重定向合并操作的目标。 通常，新目标是初始目标的嵌入父级。

 例如，在使用 "组件图" 模板创建的 DSL 中，端口嵌入在 "组件" 中。 端口在组件形状的边缘上显示为小形状。 用户通过将 "端口工具" 拖到组件形状上来创建端口。 但有时，用户错误地将端口工具拖到现有端口，而不是组件上，操作将失败。 如果有多个现有端口，这会很容易出错。 为了帮助用户避免这种干扰，你可以允许将端口拖到现有端口，但会将操作重定向到父组件。 操作的工作方式与目标元素为组件的情况相同。

 您可以在组件模型解决方案中创建向前合并指令。 如果编译并运行原始解决方案，则应会看到用户可将任意数量的**输入端口**或**输出端口**元素从 "**工具箱**" 拖动到 "**组件**" 元素。 但是，它们不能将端口拖到现有端口。 不可用指针通知它们此移动未启用。 但是，您可以创建一个向前合并指令，以便将在现有**输入端口**上无意间删除的端口转发给**Component**元素。

#### <a name="to-create-a-forward-merge-directive"></a>创建向前合并指令

1. 使用组件模型模板创建 [!INCLUDE[dsl](../includes/dsl-md.md)] 解决方案。

2. 打开 Dsldefinition.dsl，显示**Dsl 资源管理器**。

3. 在**DSL 资源管理器**中，展开 "**域类**"。

4. **ComponentPort**抽象域类是**InPort**和**OutPort**的基类。 右键单击**ComponentPort** ，然后单击 "**添加新元素合并指令**"。

     "**元素合并**指令" 节点下将显示一个新的 "**元素合并指令**" 节点。

5. 选择 "**元素合并指令**" 节点并打开 " **DSL 详细信息**" 窗口。

6. 在 "索引类" 列表中，选择 " **ComponentPort**"。

7. 选择 "**向前合并到其他域类**"。

8. 在路径选择列表中，展开 " **ComponentPort**"，展开 " **ComponentHasPorts**"，然后选择 "**组件**"。

     新路径应类似于：

     **ComponentHasPorts/！组件**

9. 保存解决方案，然后通过单击**解决方案资源管理器**工具栏上最右侧的按钮来转换这些模板。

10. 生成和运行解决方案。 此时将显示 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的新实例。

11. 在**解决方案资源管理器**中，打开 mydsl。 将显示关系图和**ComponentLanguage 工具箱**。

12. 将**输入端口**从**工具箱**拖动到另一个**输入端口。** 接下来，将**OutputPort**拖到**InputPort** ，然后拖动到另一个**OutputPort**。

     看不到不可用的指针，并且应该能够在现有的**输入端口**上删除现有的。 选择新的**输入端口**并将其拖到**组件**上的另一个点。

## <a name="see-also"></a>请参阅
 [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)[自定义工具和工具箱](../modeling/customizing-tools-and-the-toolbox.md)
