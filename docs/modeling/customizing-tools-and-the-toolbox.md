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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: da472f443f52a6478ac5e1e34fd4d4a5beb0721b
ms.sourcegitcommit: 51dad3e11d7580567673e0d426ab3b0a17584319
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66820814"
---
# <a name="customizing-tools-and-the-toolbox"></a>自定义工具和工具箱

你必须为你想要使用户添加到其模型的元素定义工具箱项。 有两种类型的工具：元素工具和连接工具。 在生成的设计器中，用户可以选择元素工具以将形状拖动到关系图中，也可以选择连接工具以在形状之间绘制链接。 通常，元素工具允许用户向其模型添加域类的实例，而连接工具允许他们添加域关系的实例。

## <a name="ToolboxDef"></a> 如何定义工具箱
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
> 若要在 DSL 资源管理器中添加或粘贴项，请右键单击新节点的祖父级。 例如，若要添加一种工具，请右键单击选项卡上，而非**工具**节点。 若要添加选项卡，右键单击**编辑器**节点。

**工具箱图标**属性的每个工具引用 16x16 位图文件。 这些文件通常保留在**Dsl\Resources**文件夹。

**类**属性元素工具引用具体域类。 默认情况下，该工具将创建此类的实例。 但是，你可以编写代码以具有用于创建元素组或不同类型的元素的工具。

**连接生成器**连接工具属性引用连接生成器，它定义该工具可以连接哪些类型的元素，以及它们之间创建哪些关系。 连接生成器将定义为 DSL 资源管理器中的节点。 在定义域关系时将自动创建连接生成器，但你可以编写代码来自定义它们。

#### <a name="to-add-a-tool-to-the-toolbox"></a>将工具添加到工具箱

1. 通常在已创建形状类并将其映射到域类后创建元素工具。

     通常在已创建连接符类并将其映射到引用关系后创建连接符工具。

2. 在 DSL 资源管理器，展开**编辑器**节点并**工具箱选项卡**节点。

     右键单击工具箱选项卡节点，然后依次**添加新元素工具**或**添加新连接工具**。

3. 设置**工具箱图标**属性来指代 16 × 16 位图。

     如果你想要定义新图标，在解决方案资源管理器中创建一个位图文件**Dsl\Resources**文件夹。 该文件应具有以下属性值：**生成操作** = **内容**;**复制到输出目录** = **不要复制**。

4. **对于元素工具：** 设置**类**属性引用映射到一个形状的具体域类的工具。

     **对于连接符工具：** 设置**连接生成器**属性到一个下拉列表中提供的项的工具。 在将连接符映射到域关系后自动创建连接生成器。 如果最近创建过连接符，则通常选择关联的连接生成器。

5. 若要测试 DSL，请按 F5 或 CTRL + F5，并在 Visual Studio 的实验实例中，打开示例模型文件。 新工具应显示在工具箱上。 将它拖动到关系图上以验证它是否将创建新元素。

     如果未显示该工具，停止实验性 Visual Studio。 在 Windows 中**启动**菜单中，运行**重置 Microsoft Visual Studio 2010 实验实例**。 在“生成”菜单上，单击“重新生成解决方案”   。 然后，再次测试 DSL。

## <a name="customizing"></a> 自定义元素工具
 默认情况下，该工具将创建指定类的单个实例，但是可通过两种方式改变这种情况：

- 在其他类上定义元素合并指令，从而允许它们接受此类的新实例，并允许它们在创建新元素后创建其他链接。 例如，你可以允许用户将“注释”放到其他元素上，从而在两个元素之间创建引用链接。

     这些自定义还将影响当用户粘贴或拖动并放置元素时将发生的情况。

     有关详细信息，请参阅[自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。

- 编写代码来自定义工具，以便它可以创建元素组。 该工具由 ToolboxHelper.cs 中可重写的方法进行初始化。 有关详细信息，请参阅[创建一个工具中的元素组](#groups)。

## <a name="groups"></a> 从一种工具创建元素组
 每个元素工具都包含它应创建的元素的原型。 默认情况下，每个元素工具都将创建单个元素，但也可以使用一个工具创建一组相关对象。 为此，请使用包含相关项的 <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> 初始化工具。

 以下示例取自 DSL，其中有晶体管类型。 每个晶体管具有三个命名的“终端”。 用于晶体管的元素工具将存储包含四个模型元素和三个关系链接的原型。 当用户将工具拖动到关系图上时，该原型将进行实例化并链接到模型根。

 此代码将重写中定义的方法**Dsl\GeneratedCode\ToolboxHelper.cs**。

 通过使用程序代码自定义模型的详细信息，请参阅[导航和更新程序代码中的模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

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

## <a name="connections"></a> 自定义连接工具
 通常，在创建新的连接符类后创建元素工具。 或者，可通过允许两个终端的类型确定关系类型来重载一个工具。 例如，可以定义一个可同时创建 Person-Person 关系和 Person-Town 关系的连接工具。

 连接工具将调用连接生成器。 使用连接生成器来指定用户在生成的设计器中链接元素的方式。 连接生成器将指定可链接的元素以及在元素之间创建的链接类型。

 在域类之间创建引用关系后，将自动创建连接生成器。 可在映射连接工具时使用此连接生成器。 有关如何创建连接工具的详细信息，请参阅[配置工具箱](../modeling/customizing-tools-and-the-toolbox.md)。

 你可以修改默认连接生成器，以便它能够处理不同范围的源和目标类型，以及创建不同类型的关系。

 还可为连接生成器编写自定义代码，以便为连接指定源和目标类、定义要进行的连接类型，以及执行与创建连接相关联的其他操作。

### <a name="the-structure-of-connection-builders"></a>连接生成器的结构
 连接生成器包含一个或多个链接连接指令，可指定域关系以及源和目标元素。 例如，在任务流解决方案模板中，可以看到**CommentReferencesSubjectsBuilder**中**DSL 资源管理器**。 此连接生成器包含一个链接连接指令名为**CommentReferencesSubjects**，这映射到域关系**CommentReferencesSubjects**。 此链接连接指令包含一个指向 `Comment` 域类的源角色指令，和一个指向 `FlowElement` 域类的目标角色指令。

### <a name="using-connection-builders-to-restrict-source-and-target-roles"></a>使用连接生成器来限制源和目标角色
 可使用连接生成器限制使某些类显示在给定域关系的源角色或目标角色中。 例如，你可能有一个与另一个域类具有域关系的基域类，但是你可能不希望该基类的所有派生类在该关系中具有相同角色。 在任务流解决方案中，有四个具体域类 (**StartPoint**，**终结点**， **MergeBranch**，和**同步**) 直接从抽象域类继承**FlowElement**，和两个具体域类 (**任务**并**ObjectInState**)，从它间接继承。 此外，还有**流动**引用关系采用**FlowElement**中其源角色和目标角色的域类。 但是的实例**终结点**域类不应是实例的源**流**关系，也应的实例不**StartPoint**类为实例的目标**流**关系。 **FlowBuilder**连接生成器包含链接连接指令名为**流**，它指定哪些域类可以扮演源角色 (**任务**， **MergeBranch**， **StartPoint**，和**同步**)，这可以扮演目标角色 (**MergeBranch**， **终结点**，并**同步**)。

### <a name="connection-builders-with-multiple-link-connect-directives"></a>具有多个链接连接指令的连接生成器
 可向连接生成器添加多个链接连接指令。 这可以帮助您隐藏的某些用户从域模型的复杂性并使**工具箱**变得过于杂乱。 可将多种不同的域关系的链接连接指令添加到单个连接生成器。 但是，应在域关系执行大致相同的函数时合并域关系。

 在任务流解决方案中，**流动**连接工具用于绘制两个实例**流**并**ObjectFlow**域关系。 **FlowBuilder**连接生成器，此外对拥有**流**链接连接指令前面所述，两个链接连接指令名为**ObjectFlow**。 这些指令指定的实例**ObjectFlow**可能的实例之间绘制关系**ObjectInState**域类的实例或**ObjectInState**的实例**任务**，但不能跨两个实例**任务**，或从实例**任务**实例**ObjectInState**。 但是的实例**流动**可能两个实例之间绘制关系**任务**。 如果编译并运行任务流解决方案时，可以看到该绘图**流动**的实例从**ObjectInState**的实例**任务**创建的实例**ObjectFlow**，但绘图**流**两个实例之间**任务**创建的实例**流**。

### <a name="custom-code-for-connection-builders"></a>为连接生成器自定义代码
 在用户界面中有四个用于定义不同类型的连接生成器的自定义的复选框：

- **自定义接受**源或目标角色指令上的复选框

- **自定义连接**源或目标角色指令上的复选框

- **使用自定义连接**连接指令上的复选框

- **是自定义**连接生成器的属性

  你必须提供一些程序代码，才能进行这些自定义。 若要发现你必须提供的代码，请检查这些框之一、单击“转换所有模板”，然后生成解决方案。 将产生一个错误报告。 双击该错误报告以查看注释，该注释解释了应添加的代码。

> [!NOTE]
> 若要添加自定义代码，请在与 GeneratedCode 文件夹中的代码文件不同的代码文件中创建分部类定义。 为避免丢失工作，不应编辑生成的代码文件。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。

#### <a name="creating-custom-connection-code"></a>创建自定义连接代码
 在每个链接连接指令，**源角色指令**选项卡将定义从哪些类型可以拖动。 同样，**目标角色指令**选项卡将定义到哪些类型可以拖动。 对于每种类型，您可以进一步指定是否允许通过设置连接 （针对该链接连接指令）**自定义接受**标志，然后提供额外的代码。

 还可自定义在进行连接时发生的情况。 例如，可自定义仅在特定类上发生来回拖动的情况、一个链接连接指令控制的所有情况，或整个 FlowBuilder 连接生成器。 对于其中每个选项，你可以在相应的级别上设置自定义标志。 在转换所有模板并尝试生成解决方案时，错误消息将使你转到位于生成代码中的注释。 这些注释将标识你必须提供的内容。

 在“组件图”示例中，将自定义用于“连接”域关系的连接生成器以限制可在端口之间进行的连接。 下图显示只能从 `OutPort` 元素到 `InPort` 元素进行连接，但可将组件互相嵌套在内。

 **从嵌套组件传入到 OutPort 的连接**

 ![连接生成器](../modeling/media/connectionbuilder_3.png)

 因此，你可能想要指定可从嵌套组件传送到 OutPort 的连接。 若要指定此类连接，您设置**使用自定义接受**上**InPort**作为源角色类型和**OutPort**作为目标角色类型**DSL 详细信息**窗口下图中所示：

 **链接连接指令在 DSL 资源管理器**

 ![连接生成器图像](../modeling/media/connectionbuilder_4a.png)

 **链接连接指令 DSL 详细信息窗口中**

 ![链接连接指令在 DSL 详细信息窗口](../modeling/media/connectionbuilder_4b.png)

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

 通过使用程序代码自定义模型的详细信息，请参阅[导航和更新程序代码中的模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

 例如，可使用相似的代码以防止用户使用父子链接创建循环。 这些限制被视为硬约束，因为用户不能违反这些在任何时间。 此外可以创建用户可以通过创建无法保存的无效配置来临时绕软验证检查。

### <a name="good-practice-in-defining-connection-builders"></a>定义连接生成器的最佳做法
 你应定义一个连接生成器来创建不同类型的关系（仅当它们在概念上相互相关时）。 在任务流示例中，请使用同一个生成器在任务之间以及在任务和对象之间创建流。 但是，使用同一个生成器在注释和任务之间创建关系可能会造成混淆。

 如果定义用于多种类型的关系的连接生成器，你应确保它不能从同一对源和目标对象与多种类型相匹配。 否则，结果将不可预知。

 使用自定义代码来应用硬约束，但应考虑用户是否应能够临时进行无效连接。 如果他们应能够如此，你可以修改约束以使连接不进行验证，直到用户尝试保存更改。

## <a name="see-also"></a>请参阅

- [自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)
- [自定义复制行为](../modeling/customizing-copy-behavior.md)
- [如何：添加拖放句柄](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [线路关系图示例 DSL](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)