---
title: 使用 UML API 编辑 UML 序列图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML activity diagrams, programming
ms.assetid: 8cdd0203-85ef-4c62-9abc-da4cb26fa504
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d0bebbb4e6dfe25ce9834595be11aad0fd1f1ba0
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871873"
---
# <a name="edit-uml-sequence-diagrams-by-using-the-uml-api"></a>使用 UML API 编辑 UML 序列图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

交互是一组生命线之间的消息序列。 交互显示在 UML 序列图上。

 有关 API 的完整详细信息, 请参阅[VisualStudio](/previous-versions/dd493373(v=vs.140))。

 有关编写用于 UML 关系图的命令和笔势处理程序的更一般的介绍, 请参阅[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。

## <a name="basic-code"></a>基本代码

### <a name="namespace-imports"></a>命名空间导入
 必须包括以下 `using` 语句：

```
using Microsoft.VisualStudio.Uml.Classes;
   // for basic UML types such as IPackage
using Microsoft.VisualStudio.Uml.Interactions;
   // for interaction types
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
   // to create elements and use additional functions
```

 如果要创建菜单命令和笔势处理程序，将还需要：

```
using System.ComponentModel.Composition;
   // for Import and Export
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
   // for ICommandExtension
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
   // for diagrams and context
```

 有关详细信息, 请参阅[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。

### <a name="getting-the-context"></a>获取上下文
 如果正在编辑作为序列图中命令或笔势处理程序一部分的交互，则可以获取对上下文的引用。 例如:

```
[SequenceDesignerExtension]
[Export(typeof(ICommandExtension))]
public class MySequenceDiagramCommand : ICommandExtension
{
    [Import]
    public IDiagramContext Context { get; set; }
    public void QueryStatus (IMenuCommand command)
    {
      ISequenceDiagram sequenceDiagram =
          Context.CurrentDiagram as ISequenceDiagram;
         ...
```

### <a name="generated-and-uml-sequence-diagrams"></a>已生成的序列图和 UML 序列图
 有两种类型的序列图：在 UML 建模项目中手动创建的序列图，以及从程序代码生成的序列图。 使用 `UmlMode` 属性来发现你所拥有的序列图。

> [!NOTE]
> 此属性仅对使用 Visual Studio 2013 及更早版本从代码生成的序列图返回 false。 这包括从 2013 及更早版本迁移的代码生成序列图。 此版本的 Visual Studio 不支持生成新序列图。

 例如，如果想要使某个菜单命令仅在 UML 序列图上可见，则 `QueryStatus()` 方法可能包括以下语句：

```
command.Enabled = command.Visible =
      sequenceDiagram != null && sequenceDiagram.UmlMode;
```

 在生成的序列图上，生命线、消息和其他元素几乎与 UML 序列图上相同。 在 UML 模型中，模型存储区具有根，且该模型拥有所有其他元素。 但生成的交互存在于其自己的模型存储区中，且具有 Null 根：

```
IModel rootModel = sequenceDiagram.ModelStore.Root;
    // !sequenceDiagram.UmlMode == (rootModel == null)
```

## <a name="to-create-and-display-an-interaction"></a>创建并显示交互
 创建作为包或模型子集的交互。

 例如，如果正在开发可能在空序列图上执行的命令，则应始终通过检查交互是否存在来开始。

```
public void Execute (IMenuCommand command)
{
    ISequenceDiagram sequenceDiagram =
         Context.CurrentDiagram as ISequenceDiagram;
    if (sequenceDiagram == null) return;
    // Get the diagram's interaction:
    IInteraction interaction = sequenceDiagram.Interaction;
    // A new sequence diagram might have no interaction:
    if (interaction == null)
    {
       // Get the home package or model of the diagram:
       IPackage parentPackage = sequenceDiagram.GetObject<IPackage>();
       interaction = parentPackage.CreateInteraction();
       // Display the interaction on the sequence diagram:
       sequenceDiagram.Bind(interaction);
    }
```

## <a name="updating-an-interaction-and-its-layout"></a>更新交互及其布局
 更新交互时，请始终通过使用以下方法之一更新其布局来结束你的操作：

- `ISequenceDiagram.UpdateShapePositions()`调整最近插入或移动的形状的位置及其相邻形状。

- `ISequenceDiagram.Layout([SequenceDiagramLayoutKinds])` 重绘整个关系图。 你可以使用该参数来指定生命线和/或消息的重新定位。

  在插入新元素或移动现有元素时，这一点尤为重要。 在执行这些操作的其中一个之前，它们将不会位于关系图上的正确位置。 你只需在一系列更改结束时调用这些操作的其中一个。

  若要避免对在命令之后执行撤消操作的用户造成困惑，请使用 `ILinkedUndoTransaction` 以包括你的更改和最终的 `Layout()` 或 `UpdateShapePositions()` 操作。 例如:

```
using (ILinkedUndoTransaction transaction = LinkedUndoContext.BeginTransaction("create loop"))
{
  Interaction.CreateCombinedFragment(InteractionOperatorKind.Loop, messages);
  Diagram.UpdateShapePositions();
  transaction.Commit();
}
```

 若要使用 `ILinkedUndoTransaction`，则必须在你的类中进行此声明：

```
[Import] ILinkedUndoContext LinkedUndoContext { get; set; }
```

 有关详细信息, 请参阅[使用事务链接 UML 模型更新](../modeling/link-uml-model-updates-by-using-transactions.md)。

## <a name="building-an-interaction"></a>生成交互

### <a name="to-create-lifelines"></a>创建生命线

```
ILifeline lifeline = interaction.CreateLifeline();
```

 生命线表示可连接的元素，即一种类型的实例。 例如，如果交互用于显示组件如何将传入消息委托给其内部部件，则生命线可表示组件的端口和部件：

```
foreach (IConnectableElement part in
            component.Parts
           .Concat<IConnectableElement>(component.OwnedPorts))
{
   ILifeline lifeline = interaction.CreateLifeline();
   lifeline.Represents = part;
}
```

 或者，如果交互显示一组任意对象，则可以在交互自身内创建属性或其他 `IConnectableElement`：

```
ILifeline lifeline = interaction.CreateLifeline();
IProperty property1 = interaction.CreateProperty();
property1.Type = model.CreateInterface();
property1.Type.Name = "Type 1";
lifeline.Represents = property1;
```

 作为进一步的替代方法，可以在不将其链接到可连接元素的情况下设置生命线的名称和类型：

```
ILifeline lifeline = interaction.CreateLifeline();
lifeline.Name = "c1";
lifeline.SetInstanceType("Customer");
System.Diagnostics.Debug.Assert(
           lifeline.GetDisplayName() == "c1:Customer"  );
```

### <a name="to-create-messages"></a>创建消息
 若要创建消息，则必须确定源生命线和目标生命线上的插入点。 例如:

```
interaction.CreateMessage( sourceInsertionPoint,
                           targetInsertionPoint,
                           MessageKind.Complete,
                           MessageSort.ASynchCall)
```

 创建具有未定义源或未定义目标的消息：

```
interaction.CreateLostFoundMessage(MessageKind.Found, insertionPoint);
```

 有几条消息可用于确定生命线上所有关键点位置的插入点：

|ILifeline 上的方法|使用它来在此点插入|
|-------------------------|------------------------------------|
|`FindInsertionPointAtTop()`|生命线的顶部。|
|`FindInsertionPointAtBottom()`|生命线的底部。|
|`FindInsertionPointAfterMessage`<br /><br /> `(IMessage previous)`|紧跟在指定消息之后的点。|
|`FindInsertionPointAfterExecutionSpecification`<br /><br /> `(IExecutionSpecification previous)`|该点可以位于生命线上，也可以位于父执行规范块上。|
|`FindInsertionPointAfterInteractionUse`<br /><br /> `(IInteractionUse previous)`|交互使用之后的点。|
|`FindInsertionPointAfterCombinedFragment`<br /><br /> `(ICombinedFragment previous)`|组合片段之后的点。|
|`FindInsertionPoint(IExecutionSpecification block)`|执行块的顶部。|
|`FindInsertionPoint(IInteractionOperand fragment)`|组合片段操作数的顶部。|

 创建消息时，请注意避免定义跨另一条消息的消息。

### <a name="to-create-combined-fragments-and-interaction-uses"></a>创建组合片段和交互使用
 你可以通过在该元素必须涵盖的每个生命线上指定插入点来创建组合片段和交互使用。 请注意避免指定一组将跨现有消息或片段的点。

```
Interaction.CreateCombinedFragment(InteractionOperatorKind.Loop,
  Interaction.Lifelines.Select(lifeline => lifeline.FindInsertionPointAtTop()));
Interaction.CreateInteractionUse(
  Interaction.Lifelines.Select(lifeline => lifeline.FindInsertionPointAtTop()));
```

 你还可以创建涵盖一组现有消息的组合片断。 消息必须全部来源于同一个生命线或执行块。

```
ICombinedFragment cf = Interaction.CreateCombinedFragment(
  InteractionOperatorKind.Loop,
  Interaction.Lifelines.First().GetAllOutgoingMessages());
```

 请始终使用单个操作数创建组合片段。 若要创建新的操作数，必须指定要在之前或之后插入的现有操作数，并指定是否希望在其之前或之后插入：

```
// Create an additional operand before the first
cf.CreateInteractionOperand(cf.Operands.First(), false);
// Create an additional operand after the last:
cf.CreateInteractionOperand(cf.Operands.Last(), true);
```

## <a name="troubleshooting"></a>疑难解答
 如果没有使用 `UpdateShapePositions()` 或 `Layout()` 操作完成更改，则形状将显示在不正确的位置。

 大多数其他问题都是由未对齐的插入点引起的，进而导致新消息或片段跨其他消息或片段。 症状可能是未执行任何更改，或者引发异常。 在执行 `UpdateShapePositions()` 或 `Layout()` 操作之前，不会引发异常。

## <a name="see-also"></a>请参阅

- [VisualStudio。](/previous-versions/dd493373(v=vs.140))
- [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)
- [在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)
- [定义自定义建模工具箱项](../modeling/define-a-custom-modeling-toolbox-item.md)
- [为 UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)
- [使用 UML API 编程](../modeling/programming-with-the-uml-api.md)
