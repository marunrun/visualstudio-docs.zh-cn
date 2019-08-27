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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f956f492c3dc690ef2edb67d9a7c75e6c0108820
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433275"
---
# <a name="customizing-element-creation-and-movement"></a>自定义元素创建和移动
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以允许元素拖动到另一种，从工具箱或中粘贴或移动操作。 您可以已移动的元素链接到目标元素中，通过使用指定的关系。  
  
 元素合并指令 (EMD) 指定一个模型元素时，会发生什么情况*合并*到另一个模型元素。 发生这种情况时：  
  
- 用户将从工具箱拖到关系图或形状。  
  
- 用户使用资源管理器或隔离舱形状中的添加菜单创建的元素。  
  
- 用户将从一个泳道项移动到另一个。  
  
- 用户将粘贴元素。  
  
- 你的程序代码调用元素合并指令。  
  
  尽管创建操作可能看起来不同的复制操作，但它们的实际工作方式相同。 添加一个元素，例如从工具箱中，它的原型进行复制。 原型中相同的方式已从另一个模型的一部分复制的元素合并到模型中。  
  
  EMD 的职责是确定如何对象组应合并到模型中的特定位置。 具体而言，它决定采用何种关系应实例化，若要将合并的组链接到模型。 您还可以自定义其设置属性并创建其他对象。  
  
  ![DSL&#45;EMD&#95;Merge](../modeling/media/dsl-emd-merge.png "DSL-EMD_Merge")  
  元素合并指令的角色  
  
  在定义嵌入关系时，会自动生成 EMD。 当用户将新的子实例添加到父，EMD 此默认设置创建的关系的实例。 可以通过添加自定义代码例如修改这些默认 EMDs。  
  
  此外可以在 DSL 定义中，可让用户拖动或粘贴合并和接收类的不同组合中添加您自己 EMDs。  
  
## <a name="defining-an-element-merge-directive"></a>定义元素合并指令  
 可以将元素合并指令添加到域类、 域关系、 形状、 连接符和关系图。 可以添加或接收的域类下在 DSL 资源管理器中找到它们。 在接收类是元素的已在模型中，并且新的或复制元素将合并到的域类。  
  
 ![DSL&#45;EMD&#95;Details](../modeling/media/dsl-emd-details.png "DSL-EMD_Details")  
  
 **索引类**是可以合并到接收类的成员的元素的域类。 除非设置索引类的子类的实例将还通过此 EMD 合并**应用到子类**为 False。  
  
 有两种类型的合并指令：  
  
- 一个**进程合并**指令指定的新元素应链接到的树的关系。  
  
- 一个**转发合并**指令将新元素重定向到另一个接收元素，通常的父级。  
  
  你可以添加自定义代码以合并指令：  
  
- 设置**使用自定义接受**添加你自己的代码来确定索引的元素的特定实例是否应合并到目标元素。 当用户拖动工具箱中时，"无效"的指针演示是否你的代码将不允许合并。  
  
   例如，你可以仅接收元素处于特定状态时允许合并。  
  
- 设置**使用自定义合并**添加提供自己的代码以定义模型执行合并时进行的更改。  
  
   例如，可以使用该模型中的新位置中的数据合并的元素中设置属性。  
  
> [!NOTE]
> 如果你编写自定义的合并代码，它会影响使用此 EMD 执行的唯一合并。 如果合并相同类型的对象，其他 EMDs 或如果没有其他自定义代码，而无需使用 EMD 创建这些对象，然后它们将不会影响你的自定义的合并代码。  
>   
> 如果你想要确保新的元素或新的关系始终处理由自定义代码，请考虑定义`AddRule`上的嵌入关系和`DeleteRule`元素的域类上。 有关详细信息，请参阅[规则将传播的更改中的模式](../modeling/rules-propagate-changes-within-the-model.md)。  
  
## <a name="example-defining-an-emd-without-custom-code"></a>示例:定义 EMD 而无需自定义代码  
 以下示例允许用户通过从工具箱拖到现有的形状拖动在同一时间创建元素和连接器。 该示例将 EMD 添加到 DSL 定义中。 在这种修改之前, 用户可以在实际应用到关系图中，但不是到现有的形状上拖动工具。  
  
 用户还可以粘贴到其他元素上的元素。  
  
#### <a name="to-let-users-create-an-element-and-a-connector-at-the-same-time"></a>若要允许用户在同一时间创建元素和连接器  
  
1. 使用创建新 DSL**最小语言**解决方案模板。  
  
    在运行此 DSL 时，它允许您创建的形状和连接线形状之间。 不能将拖动的新**ExampleElement**形状从工具箱拖到现有的形状。  
  
2. 若要允许用户将元素拖到合并`ExampleElement`形状，创建在新 EMD`ExampleElement`域类：  
  
   1. 在中**DSL 资源管理器**，展开**域类**。 右键单击`ExampleElement`，然后单击**添加新元素合并指令**。  
  
   2. 请确保**DSL 详细信息**窗口处于打开状态，以便您可以看到新 EMD 的详细信息。 (菜单：**查看**，**其他 Windows**， **DSL 详细信息**。)  
  
3. 设置**索引类**在 DSL 详细信息窗口中，若要定义哪一类别的元素可以合并到`ExampleElement`对象。  
  
    对于此示例中，选择`ExampleElements`，以便用户可以将新元素拖到现有元素上。  
  
    请注意，索引编制类将成为 EMD 在 DSL 资源管理器的名称。  
  
4. 下**通过创建链接处理合并**，添加两个路径：  
  
   1. 一个路径链接到父模型的新元素。 你需要输入的路径表达式从现有元素向上浏览通过嵌入关系到父模型。 最后，它将向其分配新元素的新链接中指定的角色。 路径是按如下所示：  
  
       `ExampleModelHasElements.ExampleModel/!ExampleModel/.Elements`  
  
   2. 另一条路径指向现有元素的新元素。 路径表达式指定的引用关系和要向其分配新元素的角色。 此路径如下所示：  
  
       `ExampleElementReferencesTargets.Sources`  
  
      路径导航工具可用于创建每个路径：  
  
   3. 下**通过在创建路径的链接处理合并**，单击 **\<添加路径 >** 。  
  
   4. 单击列表项的右侧的下拉箭头。 将显示树视图。  
  
   5. 展开树以形成你想要指定的路径中的节点。  
  
5. 测试 DSL:  
  
   1. 按 f5 键以重新生成并运行解决方案。  
  
        重新生成需要比平常较长时间，因为将从文本模板以符合新的 DSL 定义更新生成的代码。  
  
   2. 当实验实例的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]已启动，打开你的 DSL 的模型文件。 创建一些示例元素。  
  
   3. 从拖动**示例元素**工具拖到现有的形状上。  
  
        新形状就显示，并链接到现有的形状与连接器。  
  
   4. 复制现有的形状。 选择另一个形状并粘贴。  
  
        创建第一个形状的副本。  它具有新名称，并链接到连接器第二个形状。  
  
   请注意此过程中的以下几点：  
  
- 通过创建元素合并指令，您可以允许要接受任何其他元素的任何类。 在接收方的域类中，创建 EMD 和接受的域类中指定**Index 类**字段。  
  
- 通过定义路径，可以指定哪个链接应该用于连接到现有模型的新元素。  
  
     您指定的链接应包含一个嵌入关系。  
  
- EMD 影响这两种创建从工具箱以及粘贴操作。  
  
     如果您编写自定义创建新元素的代码，可以通过使用显式调用 EMD`ElementOperations.Merge`方法。 这可确保你的代码链接到模型的新元素的其他操作的方式相同。 有关详细信息，请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。  
  
## <a name="example-adding-custom-accept-code-to-an-emd"></a>示例:将自定义接受代码添加到 EMD  
 通过将自定义代码添加到 EMD，您可以定义更复杂的合并行为。 这个简单的示例可防止用户将添加到关系图的多个固定数量的元素。 该示例修改默认 EMD 附带的嵌入关系。  
  
#### <a name="to-write-custom-accept-code-to-restrict-what-the-user-can-add"></a>编写自定义接受用于限制用户可添加的代码  
  
1. 通过使用创建的 DSL**最小语言**解决方案模板。 打开 DSL 定义关系图。  
  
2. 在 DSL 资源管理器，展开**域类**， `ExampleModel`，**元素合并指令**。 选择名为的元素合并指令`ExampleElement`。  
  
     此 EMD 控制用户可以创建新`ExampleElement`在模型中，例如通过从工具箱中拖动的对象。  
  
3. 在中**DSL 详细信息**窗口中，选择**使用自定义接受**。  
  
4. 重新生成解决方案。 这将需要比平常长，因为生成的代码将从该模型进行更新。  
  
     生成错误将报告，类似于："Company.ElementMergeSample.ExampleElement 不包含一个定义为 CanMergeExampleElement..."  
  
     必须实现的方法`CanMergeExampleElement`。  
  
5. 创建新的代码文件中**Dsl**项目。 其内容替换为以下代码并将命名空间更改为你的项目的命名空间。  
  
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
  
     这个简单的示例将限制可以合并到父模型的元素数。 对于更有趣的条件，该方法可以检查任何属性，以及接收对象的链接。 它还可以检查中携带的合并元素的属性<xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype>。 有关详细信息`ElementGroupPrototypes`，请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。 有关如何编写读取模型的代码的详细信息，请参阅[导航和更新程序代码中的模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。  
  
6. 测试 DSL:  
  
    1. 按 f5 键以重新生成解决方案。 当实验实例的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]随即打开，打开你的 DSL 的实例。  
  
    2. 以下几种方式创建新元素：  
  
        1. 从拖动**示例元素**工具拖到关系图上的。  
  
        2. 在中**示例模型资源管理器**，右键单击根节点，然后单击**添加新示例元素**。  
  
        3. 复制并粘贴关系图上的元素。  
  
    3. 验证不能使用以下任一方式将四个元素添加到模型。 这是因为它们都使用元素合并指令。  
  
## <a name="example-adding-custom-merge-code-to-an-emd"></a>示例:将合并自定义代码添加到 EMD  
 在自定义的合并代码中，可以定义在用户拖动一个工具，或粘贴到元素上时，会发生什么情况。 有两种方法来定义自定义合并：  
  
1. 设置**使用自定义合并**并提供所需的代码。 你的代码替换生成的合并代码。 如果你想要彻底重定义合并的作用，请使用此选项。  
  
2. 重写`MergeRelate`方法，并选择性地`MergeDisconnect`方法。 若要执行此操作，必须设置**生成双派生**域类的属性。 你的代码可以调用基类中生成的合并代码。 如果你想要执行合并后执行其他操作，请使用此选项。  
  
   这些方法只会影响使用此 EMD 执行合并。 如果你想要影响可在其中创建合并的元素的所有方法，一种替代方法是定义`AddRule`上的嵌入关系和`DeleteRule`合并的域类上。 有关详细信息，请参阅[规则将传播的更改中的模式](../modeling/rules-propagate-changes-within-the-model.md)。  
  
#### <a name="to-override-mergerelate"></a>若要重写 MergeRelate  
  
1. 在 DSL 定义中，请确保已定义你想要将代码添加的 EMD。 如果需要，可以将路径添加和定义自定义接受代码，如前面各节中所述。  
  
2. 在 DslDefinition 关系图中，选择合并在接收类。 通常它是嵌入关系的源端的类。  
  
     例如，在从最小语言解决方案生成的 DSL，选择`ExampleModel`。  
  
3. 在中**属性**窗口中，将**生成双派生**到**true**。  
  
4. 重新生成解决方案。  
  
5. 检查的内容**Dsl\Generated Files\DomainClasses.cs**。 搜索方法名为`MergeRelate`并检查其内容。 这将帮助您编写您自己的版本。  
  
6. 在新代码文件中，编写在接收类的分部类，并重写`MergeRelate`方法。 请记住调用基方法。 例如：  
  
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
  
#### <a name="to-write-custom-merge-code"></a>若要编写自定义合并代码  
  
1. 在中**Dsl\Generated Code\DomainClasses.cs**，检查方法名为`MergeRelate`。 这些方法创建一个新的元素与现有模型之间的链接。  
  
    此外，检查方法名为`MergeDisconnect`。 这些方法取消链接时要删除的模型中的元素。  
  
2. 在中**DSL 资源管理器**，选择或创建你想要自定义元素合并指令。 在中**DSL 详细信息**窗口中，将**使用自定义合并**。  
  
    当设置此选项，**进程合并**和**向前合并**选项将被忽略。 改为使用你的代码。  
  
3. 重新生成解决方案。 由于生成的代码文件将从该模型进行更新需要比平常长。  
  
    将显示错误消息。 双击要查看生成的代码中的说明进行操作的错误消息。 这些说明要求你提供两种方法`MergeRelate` *YourDomainClass*并`MergeDisconnect` *YourDomainClass*  
  
4. 在单独的代码文件中的分部类定义中编写方法。 需检查前面的示例应建议所需内容。  
  
   自定义的合并代码将不会影响代码直接创建对象和关系并不会影响其他 EMDs。 为了确保不管如何创建元素实现其他更改，请考虑在写入`AddRule`和一个`DeleteRule`相反。 有关详细信息，请参阅[规则将传播的更改中的模式](../modeling/rules-propagate-changes-within-the-model.md)。  
  
## <a name="redirecting-a-merge-operation"></a>将合并操作重定向  
 正向合并指令将重定向为合并操作的目标。 通常情况下，新的目标是嵌入父级的初始目标。  
  
 例如，在使用组件图模板创建 DSL 中，端口被嵌入在组件中。 端口显示为小组件形状边缘上的形状。 用户通过将端口工具拖动到组件形状上创建端口。 但有时，用户会错误地将端口工具拖动到现有的端口，而不是该组件上，则操作将失败。 当有多个现有端口时，这是易犯错误。 若要帮助用户避免此给您带来麻烦，可以允许端口以拖放到现有的端口，但具有重定向到父组件的操作。 目标元素好像组件正常执行该操作。  
  
 在组件模型解决方案中，可以创建向前合并指令。 如果编译并运行原始解决方案时，你应会看到用户可以将任意数量的**输入端口**或**输出端口**中的元素**工具箱**到**组件**元素。 但是，它们不能将端口拖到现有的端口。 不可用指针提醒他们不支持此移动。 但是，您可以创建向前合并指令，以便端口，是无意中删除某个现有**输入端口**转发给**组件**元素。  
  
#### <a name="to-create-a-forward-merge-directive"></a>若要创建转发合并指令  
  
1. 创建[!INCLUDE[dsl](../includes/dsl-md.md)]解决方案使用组件模型模板。  
  
2. 显示**DSL 资源管理器**通过打开 DslDefinition.dsl。  
  
3. 在中**DSL 资源管理器**，展开**域类**。  
  
4. **ComponentPort**抽象域类是两个基类**InPort**并**OutPort**。 右键单击**ComponentPort** ，然后单击**添加新元素合并指令**。  
  
     一个新**元素合并指令**节点下显示**元素合并指令**节点。  
  
5. 选择**元素合并指令**节点，然后打开**DSL 详细信息**窗口。  
  
6. 在索引类列表中，选择**ComponentPort**。  
  
7. 选择**将合并转发到其他域类**。  
  
8. 在路径选择列表中，展开**ComponentPort**，展开**ComponentHasPorts**，然后选择**组件**。  
  
     新路径应类似于此：  
  
     **ComponentHasPorts.Component/!Component**  
  
9. 保存的解决方案，然后通过单击最右侧的按钮转换模板**解决方案资源管理器**工具栏。  
  
10. 生成和运行解决方案。 新实例[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]出现。  
  
11. 在中**解决方案资源管理器**，打开 Sample.mydsl。 在关系图并**ComponentLanguage 工具箱**出现。  
  
12. 拖动**输入端口**从**工具箱**到另一个**输入端口。** 接下来，拖**OutputPort**到**InputPort** ，然后到另一个**OutputPort**。  
  
     不应出现不可用的指针，并且应该能够删除新**输入端口**基于现有模板。 选择新**输入端口**将其拖动到另一个点**组件**。  
  
## <a name="see-also"></a>请参阅  
 [导航和更新程序代码中的模型](../modeling/navigating-and-updating-a-model-in-program-code.md)   
 [自定义工具和工具箱](../modeling/customizing-tools-and-the-toolbox.md)   
 [线路关系图示例 DSL](http://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)
