---
title: 自定义工具和工具箱
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.selectiondialog
- vs.dsltools.dsldesigner.selecticondialog
- vs.dsltools.dsldesigner.selectcursordialog
helpviewer_keywords:
- Domain-Specific Language, toolbox
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2e8e9fc3a9ecbadc47c3390d2d4a9b504a316658
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589716"
---
# <a name="customizing-tools-and-the-toolbox"></a>自定义工具和工具箱

你必须为你想要使用户添加到其模型的元素定义工具箱项。 有两种类型的工具：元素工具和连接工具。 在生成的设计器中，用户可以选择元素工具以将形状拖动到关系图中，也可以选择连接工具以在形状之间绘制链接。 通常，元素工具允许用户向其模型添加域类的实例，而连接工具允许他们添加域关系的实例。

## <a name="ToolboxDef"></a>如何定义工具箱
 在 DSL 资源管理器中，展开“编辑器”节点及其下面的节点。 通常，你将看到如下所示的层次结构：

```
Editor
     Toobox Tabs
        MyDsl          //a tab
           Tools
               ExampleElement      // an element tool
               ExampleRelationship // a connection tool
```

在 DSL 资源管理器的此部分中，你可以执行以下操作：

- 创建新选项卡。 选项卡定义工具箱中的节标题。

- 创建新工具。

- 复制和粘贴工具。

- 在列表中上移或下移工具。

- 删除选项卡和工具。

> [!IMPORTANT]
> 若要在 DSL 资源管理器中添加或粘贴项，请右键单击新节点的祖父级。 例如，若要添加工具，请右键单击该选项卡，而不是 "**工具**" 节点。 若要添加选项卡，请右键单击**编辑器**节点。

每个工具的 "**工具箱" 图标**属性都引用16x16 位图文件。 这些文件通常保存在**Dsl\Resources**文件夹中。

元素工具的**Class**属性引用具体域类。 默认情况下，该工具将创建此类的实例。 但是，你可以编写代码以具有用于创建元素组或不同类型的元素的工具。

连接工具的 "**连接生成器**" 属性指的是一个连接生成器，它定义该工具可连接的元素类型以及它在它们之间创建的关系。 连接生成器将定义为 DSL 资源管理器中的节点。 在定义域关系时将自动创建连接生成器，但你可以编写代码来自定义它们。

#### <a name="to-add-a-tool-to-the-toolbox"></a>将工具添加到工具箱

1. 通常在已创建形状类并将其映射到域类后创建元素工具。

     通常在已创建连接符类并将其映射到引用关系后创建连接符工具。

2. 在 "DSL 资源管理器" 中，展开 "**编辑器**" 节点和 "**工具箱" 选项卡**节点。

     右键单击 "工具箱" 选项卡节点，然后单击 "**添加新元素工具**" 或 "**添加新连接工具**"。

3. 设置 "**工具箱" 图标**属性以引用16x16 位图。

     如果要定义新图标，请在**Dsl\Resources**文件夹的解决方案资源管理器中创建一个位图文件。 该文件应具有以下属性值：**生成操作** = **内容**;**复制到输出目录** = **不复制**。

4. **对于元素工具：** 设置工具的 "**类**" 属性，以引用映射到形状的具体域类。

     **对于连接器工具：** 将工具的 "**连接生成器**" 属性设置为下拉列表中提供的一项。 在将连接符映射到域关系后自动创建连接生成器。 如果最近创建过连接符，则通常选择关联的连接生成器。

5. 若要测试 DSL，请按 F5 或 CTRL + F5，并在 Visual Studio 的实验实例中打开示例模型文件。 新工具应显示在工具箱上。 将它拖动到关系图上以验证它是否将创建新元素。

     如果该工具未出现，则停止实验性的 Visual Studio。 在 Windows "**开始**" 菜单中，运行 **"重置 Microsoft Visual Studio 2010 实验实例"** 。 在“生成”菜单上，单击“重新生成解决方案”。 然后，再次测试 DSL。

## <a name="customizing"></a>自定义元素工具
 默认情况下，该工具将创建指定类的单个实例，但是可通过两种方式改变这种情况：

- 在其他类上定义元素合并指令，从而允许它们接受此类的新实例，并允许它们在创建新元素后创建其他链接。 例如，你可以允许用户将“注释”放到其他元素上，从而在两个元素之间创建引用链接。

     这些自定义还将影响当用户粘贴或拖动并放置元素时将发生的情况。

     有关详细信息，请参阅[自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。

- 编写代码来自定义工具，以便它可以创建元素组。 该工具由 ToolboxHelper.cs 中可重写的方法进行初始化。 有关详细信息，请参阅[从工具创建元素组](#groups)。

## <a name="groups"></a>从工具创建元素组
 每个元素工具都包含它应创建的元素的原型。 默认情况下，每个元素工具都将创建单个元素，但也可以使用一个工具创建一组相关对象。 为此，请使用包含相关项的 <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> 初始化工具。

 以下示例取自 DSL，其中有晶体管类型。 每个晶体管具有三个命名的“终端”。 用于晶体管的元素工具将存储包含四个模型元素和三个关系链接的原型。 当用户将工具拖动到关系图上时，该原型将进行实例化并链接到模型根。

 此代码将重写在**Dsl\GeneratedCode\ToolboxHelper.cs**中定义的方法。

 有关使用程序代码自定义模型的详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

```
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;

  public partial class CircuitsToolboxHelper
  {
    /// <summary>
    /// Toolbox initialization, called for each element tool on the toolbox.
    /// This version deals with each Component subtype separately.
    /// </summary>
    /// <param name="store"></param>
    /// <param name="domainClassId">Identifies the domain class this tool should instantiate.</param>
    /// <returns>prototype of the object or group of objects to be created by tool</returns>
    protected override ElementGroupPrototype CreateElementToolPrototype(Store store, Guid domainClassId)
    {
        if (domainClassId == Transistor.DomainClassId)
        {
            Transistor transistor = new Transistor(store);

            transistor.Base = new ComponentTerminal(store);
            transistor.Collector = new ComponentTerminal(store);
            transistor.Emitter = new ComponentTerminal(store);

            transistor.Base.Name = "base";
            transistor.Collector.Name = "collector";
            transistor.Emitter.Name = "emitter";

            // Create an ElementGroup for the Toolbox.
            ElementGroup elementGroup = new ElementGroup(store.DefaultPartition);
            elementGroup.AddGraph(transistor, true);
            // AddGraph includes the embedded parts

            return elementGroup.CreatePrototype();
        }
        else
        {
            return base.CreateElementToolPrototype(store, domainClassId);
}  }    }
```

## <a name="connections"></a>自定义连接工具
 通常，在创建新的连接符类后创建元素工具。 或者，可通过允许两个终端的类型确定关系类型来重载一个工具。 例如，可以定义一个可同时创建 Person-Person 关系和 Person-Town 关系的连接工具。

 连接工具将调用连接生成器。 使用连接生成器来指定用户在生成的设计器中链接元素的方式。 连接生成器将指定可链接的元素以及在元素之间创建的链接类型。

 在域类之间创建引用关系后，将自动创建连接生成器。 可在映射连接工具时使用此连接生成器。 有关如何创建连接工具的详细信息，请参阅[配置工具箱](../modeling/customizing-tools-and-the-toolbox.md)。

 你可以修改默认连接生成器，以便它能够处理不同范围的源和目标类型，以及创建不同类型的关系。

 还可为连接生成器编写自定义代码，以便为连接指定源和目标类、定义要进行的连接类型，以及执行与创建连接相关联的其他操作。

### <a name="the-structure-of-connection-builders"></a>连接生成器的结构
 连接生成器包含一个或多个链接连接指令，可指定域关系以及源和目标元素。 例如，在 "任务流" 解决方案模板中，可在**DSL 资源管理器**中查看**CommentReferencesSubjectsBuilder** 。 此连接生成器包含一个名为**CommentReferencesSubjects**的链接连接指令，该指令映射到域关系**CommentReferencesSubjects**。 此链接连接指令包含一个指向 `Comment` 域类的源角色指令，和一个指向 `FlowElement` 域类的目标角色指令。

### <a name="using-connection-builders-to-restrict-source-and-target-roles"></a>使用连接生成器来限制源和目标角色
 可使用连接生成器限制使某些类显示在给定域关系的源角色或目标角色中。 例如，你可能有一个与另一个域类具有域关系的基域类，但是你可能不希望该基类的所有派生类在该关系中具有相同角色。 在任务流解决方案中，有四个具体的域类（**StartPoint**、 **EndPoint**、 **MergeBranch**和**同步**）直接从抽象域类**FlowElement**继承，另外两个具体域类（**Task**和**ObjectInState**）从它间接继承。 还存在一个在其源角色和目标角色中采用**FlowElement**域类的**流**引用关系。 但是，**终结点**域类的实例不应是**flow**关系的实例的源，也不应是**StartPoint**类的实例作为**flow**关系的实例的目标。 **FlowBuilder**连接生成器具有一个名为**Flow**的链接连接指令，该指令指定哪些域类可以扮演源角色（**任务**、 **MergeBranch**、 **StartPoint**和**同步**），并可以播放目标角色（**MergeBranch**、 **Endpoint**和**同步**）。

### <a name="connection-builders-with-multiple-link-connect-directives"></a>具有多个链接连接指令的连接生成器
 可向连接生成器添加多个链接连接指令。 这可以帮助用户隐藏用户的某些复杂的域模型，并使**工具箱**变得过于杂乱。 可将多种不同的域关系的链接连接指令添加到单个连接生成器。 但是，应在域关系执行大致相同的函数时合并域关系。

 在任务流解决方案中，**流**连接工具用于绘制**流**和**ObjectFlow**域关系的实例。 除了前面所述的**流**链接连接指令， **FlowBuilder**连接生成器还具有名为**ObjectFlow**的两个链接连接指令。 这些指令指定**ObjectFlow**关系的实例可以在**ObjectInState**域类的实例之间进行绘制，或在**ObjectInState**的实例之间**绘制，而**不是在任务的两个实例之间绘制，而不是在**任务**的实例或从**任务**的实例到**ObjectInState**的实例之间进行绘制。 但是，可以在**任务**的两个实例之间绘制**流**关系的实例。 如果编译并运行任务流解决方案，可以看到从**ObjectInState**实例到**任务**实例的**流**将创建**ObjectFlow**的实例，但在两个**任务**实例之间绘制**流**将创建**流**的实例。

### <a name="custom-code-for-connection-builders"></a>为连接生成器自定义代码
 在用户界面中有四个用于定义不同类型的连接生成器的自定义的复选框：

- 源或目标角色指令上的 "**自定义接受**" 复选框

- 源或目标角色指令上的 "**自定义连接**" 复选框

- connect 指令上的 "**使用自定义连接**" 复选框

- 连接生成器的**自定义**属性

  你必须提供一些程序代码，才能进行这些自定义。 若要发现你必须提供的代码，请检查这些框之一、单击“转换所有模板”，然后生成解决方案。 将产生一个错误报告。 双击该错误报告以查看注释，该注释解释了应添加的代码。

> [!NOTE]
> 若要添加自定义代码，请在与 GeneratedCode 文件夹中的代码文件不同的代码文件中创建分部类定义。 为避免丢失工作，不应编辑生成的代码文件。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。

#### <a name="creating-custom-connection-code"></a>创建自定义连接代码
 在每个链接连接指令中，"**源角色指令**" 选项卡定义了可拖动的类型。 同样，"**目标角色指令**" 选项卡定义了可拖动的类型。 对于每种类型，您可以通过设置**自定义接受**标志并提供额外的代码，进一步指定是否允许连接（对于该链接连接指令）。

 还可自定义在进行连接时发生的情况。 例如，可自定义仅在特定类上发生来回拖动的情况、一个链接连接指令控制的所有情况，或整个 FlowBuilder 连接生成器。 对于其中每个选项，你可以在相应的级别上设置自定义标志。 在转换所有模板并尝试生成解决方案时，错误消息将使你转到位于生成代码中的注释。 这些注释将标识你必须提供的内容。

 在“组件图”示例中，将自定义用于“连接”域关系的连接生成器以限制可在端口之间进行的连接。 下图显示只能从 `OutPort` 元素到 `InPort` 元素进行连接，但可将组件互相嵌套在内。

 **从嵌套组件传入到 OutPort 的连接**

 ![连接生成器](../modeling/media/connectionbuilder_3.png)

 因此，你可能想要指定可从嵌套组件传送到 OutPort 的连接。 若要指定此类连接，请在 " **DSL 详细信息**" 窗口中将 " **InPort** " 类型上的 "**自定义接受**" 设置为 "源角色"，并将 " **OutPort**类型" 指定为 "目标角色"，如以下

 **DSL 资源管理器中的链接连接指令**

 ![连接生成器图像](../modeling/media/connectionbuilder_4a.png)

 **"DSL 详细信息" 窗口中的链接连接指令**

 !["DSL 详细信息" 窗口中的链接连接指令](../modeling/media/connectionbuilder_4b.png)

 然后，必须在 ConnectionBuilder 类中提供方法：

```
  public partial class ConnectionBuilder
  {
    /// <summary>
    /// OK if this component has children
    /// </summary>
    private static bool CanAcceptInPortAsSource(InPort candidate)
    {
       return candidate.Component.Children.Count > 0;
    }

    /// <summary>
    /// Only if source is on parent of target.
    /// </summary>
    private static bool CanAcceptInPortAndInPortAsSourceAndTarget                (InPort sourceInPort, InPort targetInPort)
    {
      return sourceInPort.Component == targetInPort.Component.Parent;
    }
// And similar for OutPorts...
```

 有关使用程序代码自定义模型的详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

 例如，可使用相似的代码以防止用户使用父子链接创建循环。 这些限制被视为 "硬" 约束，因为用户在任何时候都不能违反这些限制。 你还可以创建 "软" 验证检查，用户可以通过创建无法保存的无效配置来暂时绕过这些检查。

### <a name="good-practice-in-defining-connection-builders"></a>定义连接生成器的最佳做法
 你应定义一个连接生成器来创建不同类型的关系（仅当它们在概念上相互相关时）。 在任务流示例中，请使用同一个生成器在任务之间以及在任务和对象之间创建流。 但是，使用同一个生成器在注释和任务之间创建关系可能会造成混淆。

 如果定义用于多种类型的关系的连接生成器，你应确保它不能从同一对源和目标对象与多种类型相匹配。 否则，结果将不可预知。

 您可以使用自定义代码应用 "硬" 约束，但应考虑用户是否应该能够暂时建立无效的连接。 如果他们应能够如此，你可以修改约束以使连接不进行验证，直到用户尝试保存更改。

## <a name="see-also"></a>另请参阅

- [自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)
- [自定义复制行为](../modeling/customizing-copy-behavior.md)
- [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [线路示例 DSL](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)
