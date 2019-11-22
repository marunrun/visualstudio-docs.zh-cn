---
title: Customizing Tools and the Toolbox | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.selectiondialog
- vs.dsltools.dsldesigner.selecticondialog
- vs.dsltools.dsldesigner.selectcursordialog
helpviewer_keywords:
- Domain-Specific Language, toolbox
ms.assetid: 2a0d03d7-ebc6-4458-b9f4-d2cb8418a62d
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2a5e2a46a2326c123d6b7b4e85fa29908ede9fc9
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299330"
---
# <a name="customizing-tools-and-the-toolbox"></a>自定义工具和工具箱
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你必须为你想要使用户添加到其模型的元素定义工具箱项。 有两种类型的工具：元素工具和连接工具。 在生成的设计器中，用户可以选择元素工具以将形状拖动到关系图中，也可以选择连接工具以在形状之间绘制链接。 通常，元素工具允许用户向其模型添加域类的实例，而连接工具允许他们添加域关系的实例。

 在本主题中：

- [How the Toolbox is Defined](#ToolboxDef)

- [自定义元素工具](#customizing)

- [Creating Groups of Elements from a Tool](#groups)

- [Customizing Connection Tools](#connections)

## <a name="ToolboxDef"></a> How the toolbox is defined
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
> 若要在 DSL 资源管理器中添加或粘贴项，请右键单击新节点的祖父级。 For example, to add a tool, right-click the tab, and not the **Tools** node. To add a tab, right-click the **Editor** node.

 The **Toolbox Icon** property of every tool references a 16x16 bitmap file. These files are usually kept in the **Dsl\Resources** folder.

 The **Class** property of an element tool refers to a concrete domain class. 默认情况下，该工具将创建此类的实例。 但是，你可以编写代码以具有用于创建元素组或不同类型的元素的工具。

 The **Connection Builder** property of a connection tool refers to a connection builder, which defines what types of elements the tool can connect, and what relationships it creates between them. 连接生成器将定义为 DSL 资源管理器中的节点。 在定义域关系时将自动创建连接生成器，但你可以编写代码来自定义它们。

#### <a name="to-add-a-tool-to-the-toolbox"></a>将工具添加到工具箱

1. 通常在已创建形状类并将其映射到域类后创建元素工具。

     通常在已创建连接符类并将其映射到引用关系后创建连接符工具。

2. In DSL Explorer, expand the **Editor** node and the **Toolbox Tabs** node.

     Right-click a toolbox tab node, and then click **Add New Element Tool** or **Add New Connection Tool**.

3. Set the **Toolbox Icon** property to refer to a 16x16 bitmap.

     If you want to define a new icon, create a bitmap file in Solution Explorer in the **Dsl\Resources** folder. The file should have the following property values: **Build Action** = **Content**; **Copy to Output Directory** = **Do not copy**.

4. **For an element tool:** Set the **Class** property of the tool to refer to a concrete domain class that is mapped to a shape.

     **For a connector tool:** Set the **Connection Builder** property of the tool to one of the items that are offered in the drop-down list. 在将连接符映射到域关系后自动创建连接生成器。 如果最近创建过连接符，则通常选择关联的连接生成器。

5. 若要测试 DSL，请按 F5 或 CTRL+F5，并在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例中，打开示例模型文件。 新工具应显示在工具箱上。 将它拖动到关系图上以验证它是否将创建新元素。

     如果该工具未显示，请停止该实验 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 In the Windows **Start** menu, run **Reset the Microsoft Visual Studio 2010 Experimental Instance**. On the [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**Build** menu, click **Rebuild Solution**. 然后，再次测试 DSL。

## <a name="customizing"></a> Customizing Element Tools
 默认情况下，该工具将创建指定类的单个实例，但是可通过两种方式改变这种情况：

- 在其他类上定义元素合并指令，从而允许它们接受此类的新实例，并允许它们在创建新元素后创建其他链接。 例如，你可以允许用户将“注释”放到其他元素上，从而在两个元素之间创建引用链接。

     这些自定义还将影响当用户粘贴或拖动并放置元素时将发生的情况。

     For more information, see [Customizing Element Creation and Movement](../modeling/customizing-element-creation-and-movement.md).

- 编写代码来自定义工具，以便它可以创建元素组。 该工具由 ToolboxHelper.cs 中可重写的方法进行初始化。 For more information, see [Creating Groups of Elements from a Tool](#groups).

## <a name="groups"></a> Creating Groups of Elements from a Tool
 每个元素工具都包含它应创建的元素的原型。 默认情况下，每个元素工具都将创建单个元素，但也可以使用一个工具创建一组相关对象。 为此，请使用包含相关项的 <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> 初始化工具。

 以下示例取自 DSL，其中有晶体管类型。 每个晶体管具有三个命名的“终端”。 用于晶体管的元素工具将存储包含四个模型元素和三个关系链接的原型。 当用户将工具拖动到关系图上时，该原型将进行实例化并链接到模型根。

 This code overrides a method that is defined in **Dsl\GeneratedCode\ToolboxHelper.cs**.

 For more information about customizing the model by using program code, see [Navigating and Updating a Model in Program Code](../modeling/navigating-and-updating-a-model-in-program-code.md).

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

## <a name="connections"></a> Customizing Connection Tools
 通常，在创建新的连接符类后创建元素工具。 或者，可通过允许两个终端的类型确定关系类型来重载一个工具。 例如，可以定义一个可同时创建 Person-Person 关系和 Person-Town 关系的连接工具。

 连接工具将调用连接生成器。 使用连接生成器来指定用户在生成的设计器中链接元素的方式。 连接生成器将指定可链接的元素以及在元素之间创建的链接类型。

 在域类之间创建引用关系后，将自动创建连接生成器。 可在映射连接工具时使用此连接生成器。 For more information about how to create connection tools, see [Configuring the Toolbox](../modeling/customizing-tools-and-the-toolbox.md).

 你可以修改默认连接生成器，以便它能够处理不同范围的源和目标类型，以及创建不同类型的关系。

 还可为连接生成器编写自定义代码，以便为连接指定源和目标类、定义要进行的连接类型，以及执行与创建连接相关联的其他操作。

### <a name="the-structure-of-connection-builders"></a>连接生成器的结构
 连接生成器包含一个或多个链接连接指令，可指定域关系以及源和目标元素。 For example, in the Task Flow solution template, you can see the **CommentReferencesSubjectsBuilder** in the **DSL Explorer**. This connection builder contains one link connect directive named **CommentReferencesSubjects**, which is mapped to the domain relationship **CommentReferencesSubjects**. 此链接连接指令包含一个指向 `Comment` 域类的源角色指令，和一个指向 `FlowElement` 域类的目标角色指令。

### <a name="using-connection-builders-to-restrict-source-and-target-roles"></a>使用连接生成器来限制源和目标角色
 可使用连接生成器限制使某些类显示在给定域关系的源角色或目标角色中。 例如，你可能有一个与另一个域类具有域关系的基域类，但是你可能不希望该基类的所有派生类在该关系中具有相同角色。 In the Task Flow solution, there are four concrete domain classes (**StartPoint**, **EndPoint**, **MergeBranch**, and **Synchronization**) that inherit directly from the abstract domain class **FlowElement**, and two concrete domain classes (**Task** and **ObjectInState**) that inherit indirectly from it. There is also a **Flow** reference relationship that takes **FlowElement** domain classes in both its source role and target role. However, an instance of an **EndPoint** domain class should not be the source of an instance of a **Flow** relationship, nor should an instance of a **StartPoint** class be the target of an instance of a **Flow** relationship. The **FlowBuilder** connection builder has a link connect directive named **Flow** that specifies which domain classes can play the source role (**Task**, **MergeBranch**, **StartPoint**, and **Synchronization**) and which can play the target role(**MergeBranch**, **Endpoint**, and **Synchronization**).

### <a name="connection-builders-with-multiple-link-connect-directives"></a>具有多个链接连接指令的连接生成器
 可向连接生成器添加多个链接连接指令。 This can help you hide some of the complexities of the domain model from users and keep the **Toolbox** from getting too cluttered. 可将多种不同的域关系的链接连接指令添加到单个连接生成器。 但是，应在域关系执行大致相同的函数时合并域关系。

 In the Task Flow solution, the **Flow** connection tool is used to draw instances of both the **Flow** and the **ObjectFlow** domain relationships. The **FlowBuilder** connection builder has, in addition to the **Flow** link connect directive described earlier, two link connect directives named **ObjectFlow**. These directives specify that an instance of an **ObjectFlow** relationship may be drawn between instances of the **ObjectInState** domain class, or from an instance of an **ObjectInState** to an instance of a **Task**, but not between two instances of a **Task**, or from an instance of a **Task** to an instance of an **ObjectInState**. However, an instance of a **Flow** relationship may be drawn between two instances of a **Task**. If you compile and run the Task Flow solution, you can see that drawing a **Flow** from an instance of an **ObjectInState** to an instance of a **Task** creates an instance of an **ObjectFlow**, but drawing a **Flow** between two instances of a **Task** creates an instance of a **Flow**.

### <a name="custom-code-for-connection-builders"></a>为连接生成器自定义代码
 在用户界面中有四个用于定义不同类型的连接生成器的自定义的复选框：

- the **Custom accept** check box on a source or target role directive

- the **Custom connect** check box on a source or target role directive

- the **Uses custom connect** check box on a connect directive

- the **Is Custom** property of the connection builder

  你必须提供一些程序代码，才能进行这些自定义。 若要发现你必须提供的代码，请检查这些框之一、单击“转换所有模板”，然后生成解决方案。 将产生一个错误报告。 双击该错误报告以查看注释，该注释解释了应添加的代码。

> [!NOTE]
> 若要添加自定义代码，请在与 GeneratedCode 文件夹中的代码文件不同的代码文件中创建分部类定义。 为避免丢失工作，不应编辑生成的代码文件。 For more information, see [Overriding and Extending the Generated Classes](../modeling/overriding-and-extending-the-generated-classes.md).

#### <a name="creating-custom-connection-code"></a>创建自定义连接代码
 In each link connect directive, the **Source role directives** tab defines from what types you can drag. Similarly, the **Target role directives** tab defines to what types you can drag. For each type, you can further specify whether to allow the connection (for that link connect directive) by setting the **Custom Accept** flag and then supplying the extra code.

 还可自定义在进行连接时发生的情况。 例如，可自定义仅在特定类上发生来回拖动的情况、一个链接连接指令控制的所有情况，或整个 FlowBuilder 连接生成器。 对于其中每个选项，你可以在相应的级别上设置自定义标志。 在转换所有模板并尝试生成解决方案时，错误消息将使你转到位于生成代码中的注释。 这些注释将标识你必须提供的内容。

 在“组件图”示例中，将自定义用于“连接”域关系的连接生成器以限制可在端口之间进行的连接。 下图显示只能从 `OutPort` 元素到 `InPort` 元素进行连接，但可将组件互相嵌套在内。

 **Connection Coming in to an OutPort from a Nested Component**

 ![Connection Builder](../modeling/media/connectionbuilder-3.png "ConnectionBuilder_3")

 因此，你可能想要指定可从嵌套组件传送到 OutPort 的连接。 To specify such a connection, you set **Uses Custom Accept** on the **InPort** type as source role and the **OutPort** type as target role in the **DSL Details** window as shown in the following illustrations:

 **Link Connect Directive in DSL Explorer**

 ![Connection builder image](../modeling/media/connectionbuilder-4a.png "ConnectionBuilder_4a")

 **Link Connect Directive in DSL Details Window**

 ![](../modeling/media/connectionbuilder-4b.png "ConnectionBuilder_4b")

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
    private static bool CanAcceptInPortAndInPortAsSourceAndTarget                (InPort sourceInPort, InPort targetInPort)
    {
      return sourceInPort.Component == targetInPort.Component.Parent;
    }
// And similar for OutPorts…
```

 For more information about customizing the model by using program code, see [Navigating and Updating a Model in Program Code](../modeling/navigating-and-updating-a-model-in-program-code.md).

 例如，可使用相似的代码以防止用户使用父子链接创建循环。 将这些限制视为“硬”约束，因为用户在任何时候都不能违反这些约束。 还可创建“软”验证检查，用户可通过创建无法保存的无效配置来临时绕过这些检查。

### <a name="good-practice-in-defining-connection-builders"></a>定义连接生成器的最佳做法
 你应定义一个连接生成器来创建不同类型的关系（仅当它们在概念上相互相关时）。 在任务流示例中，请使用同一个生成器在任务之间以及在任务和对象之间创建流。 但是，使用同一个生成器在注释和任务之间创建关系可能会造成混淆。

 如果定义用于多种类型的关系的连接生成器，你应确保它不能从同一对源和目标对象与多种类型相匹配。 否则，结果将不可预知。

 可使用自定义代码来应用“硬”约束，但你应该考虑用户是否应能够临时进行无效连接。 如果他们应能够如此，你可以修改约束以使连接不进行验证，直到用户尝试保存更改。

## <a name="see-also"></a>请参阅
 [Customizing Element Creation and Movement](../modeling/customizing-element-creation-and-movement.md) [Customizing Copy Behavior](../modeling/customizing-copy-behavior.md) [How to: Add a Drag-and-Drop Handler](../modeling/how-to-add-a-drag-and-drop-handler.md) [Navigating and Updating a Model in Program Code](../modeling/navigating-and-updating-a-model-in-program-code.md)
