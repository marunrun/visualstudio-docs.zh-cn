---
title: 导航 UML 模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API
ms.assetid: 6d789b6d-2aa9-4ceb-92c4-84a300065a76
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c98aefb5e3dc0090338233ca5b05b4ebc6460719
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871778"
---
# <a name="navigate-the-uml-model"></a>导航 UML 模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍 UML 模型的主要类型。

## <a name="the-model-elements-model-and-model-store"></a>模型元素、模型和模型库
 在程序集**VisualStudio**中定义的类型对应于[Uml 规范2.1.2 版本](http://www.omg.org/spec/UML/2.1.2/Superstructure/PDF/)中定义的类型。

 UML 规范中的类型在 Visual Studio 中作为接口实现。 字母“I”附加在每个类型的名称之前。 例如：[IElement](/previous-versions/dd516035(v=vs.140))、 [IClass](/previous-versions/dd523539%28v%3dvs.140%29)、 [IOperation](/previous-versions/dd481186(v=vs.140))。

 除 IElement 之外的所有类型都从一个或多个超类型继承属性。

- 有关模型类型的摘要, 请参阅[UML 模型元素类型](../modeling/uml-model-element-types.md)。

- 有关 API 的完整详细信息, 请参阅[UML 建模扩展性的 Api 参考](../modeling/api-reference-for-uml-modeling-extensibility.md)。

### <a name="relationships"></a>关系
 UML 规范中定义的属性和关系将作为 .NET 属性实现。

 大多数关系都可以双向导航。 一个关系对应于一对属性，类型的两端各为其中一个属性。 例如，属性 `IElement.Owner` 和 `IElement.OwnedElements` 表示关系的两端。 因此，该表达式的计算结果将始终为 true：

 `IElement c; ...  c.OwnedElements.All(x => x.Owner == c)`

 许多关系（例如 IAssociation）也可由一个可以具有自己的属性的对象表示。

 如果从模型中删除某个元素，则将自动删除该元素参与的任何关系，并将更新位于另一端的属性。

 如果 UML 规范为某个属性分配多重性 0..1，则该属性的值可能为 `null`。 最大值大于1的重数表示 .NET 属性具有类型:`IEnumerable<`*键入*`>`。

 有关遍历关系的详细信息, 请参阅[与 UML API 导航关系](../modeling/navigate-relationships-with-the-uml-api.md)。

### <a name="the-ownership-tree"></a>所有权树
 模型包含[IElement](/previous-versions/dd516035(v=vs.140))对象的树。 每个元素都具有属性 `OwnedElements` 和 `Owner`。

 在大多数情况下，`Owner` 和 `OwnedElements` 属性的目标也由具有更具体的名称的其他属性引用。 例如，每个 UML 操作都由一个 UML 类所有。 因此, [IOperation](/previous-versions/dd481186(v=vs.140))有一个名为[IOperation](/previous-versions/dd473473%28v%3dvs.140%29)的属性, 以及每个[IOperation](/previous-versions/dd481186(v=vs.140))对象`Class == Owner`中的属性。

 没有所有者的树的最顶层元素是`AuxiliaryConstructs.IModel`。 IModel 包含`IModelStore`在中, 其中是[IModelStore](/previous-versions/ee789368(v=vs.140))。

 创建的每个模型元素都有一个所有者。 有关详细信息, 请参阅[在 UML 模型中创建元素和关系](../modeling/create-elements-and-relationships-in-uml-models.md)。

 ![类图：模型、关系图、形状和元素](../modeling/media/uml-mm1.png)

## <a name="shapes-and-diagrams"></a>形状和关系图
 UML 模型中的元素可以在关系图中显示。 不同类型的关系图可以显示 IElement 的不同子类型。

 在某些情况下，一个元素可以在多个关系图中显示。 例如，一个 IUseCase 元素可以具有多个 IShape，这些 IShape 可以在一个关系图或不同关系图中显示。

 形状在树中排列。 树的边缘由 ParentShape 和 ChildShapes 属性表示。 关系图是唯一没有父级的形状。 关系图图面上的形状由更小的部件组成。 例如，一个类形状具有特性和操作的隔离舱。

 有关形状的详细信息, 请参阅[在关系图上显示 UML 模型](../modeling/display-a-uml-model-on-diagrams.md)。

## <a name="access-to-the-model-in-extensions"></a>对扩展中的模型的访问
 在定义为 MEF 组件的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展中，可以声明用于从运行扩展的上下文中导入信息的属性。

|特性类型|由此可以访问的对象|详细信息|
|--------------------|----------------------------------|----------------------|
|Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation<br /><br /> .IDiagramContext<br /><br /> （在 Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll 中）|当前焦点关系图。|[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|
|Microsoft.VisualStudio.Modeling.ExtensionEnablement<br /><br /> .ILinkedUndoContext<br /><br /> （在 Microsoft.VisualStudio.Modeling.Sdk.[版本].dll 中）|允许你将更改组合成事务。|[使用事务链接 UML 模型更新](../modeling/link-uml-model-updates-by-using-transactions.md)|
|Microsoft.VisualStudio.Shell .SVsServiceProvider<br /><br /> （在 Microsoft.VisualStudio.Shell.Immutable.[版本].dll 中）|主机 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 可以从中访问文件、项目和其他方面。|[使用 Visual Studio API 打开 UML 模型](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)|

### <a name="to-get-the-context"></a>获取上下文
 在扩展类中声明下面的一个或两个接口：

```
[Import] public IDiagramContext DiagramContext { get; set; }

```

 Managed Extensibility Framework (MEF) 会将这些接口绑定到一些定义，你可以从这些定义中获取当前关系图、模型库、根对象等：

```
IDiagram diagram = this.DiagramContext.CurrentDiagram;
IClassDiagram classDiagram = diagram as IClassDiagram;
       // or diagrams of other types
IModelStore modelStore = diagram.ModelStore;
IModel model = modelStore.Root;
foreach (IDiagram diagram in modelStore.Diagrams) {...}
foreach (IElement element in modelStore.AllInstances<IUseCase>) {...}
```

### <a name="to-get-the-current-selection"></a>获取当前选择

```
// All selected shapes and their elements
foreach (IShape shape in diagram.SelectedShapes)
{
   IDiagram selectedDiagram = shape as IDiagram;
   if (selectedDiagram != null)
   { // no shape selected - user right-clicked the diagram
     ... Context.CurrentDiagram ...
   }
   else
   {
     IElement selectedElement = shape.Element;
   ...}
// All selected shapes that display a specfic type of element
foreach (IShape<IInterface> in
   diagram.GetSelectedShapes<IInterface>())
{...}
```

## <a name="accessing-another-model-or-diagrams"></a>访问另一个模型或关系图
 你可以：

- 使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 模型总线在不同模型中的元素之间创建链接。 有关详细信息, 请参阅将[UML 模型与其他模型和工具集成](../modeling/integrate-uml-models-with-other-models-and-tools.md)。

- 在只读模式下加载建模项目和关系图，而不使其在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 用户界面中可见。 有关详细信息, 请参阅[在程序代码中读取 UML 模型](../modeling/read-a-uml-model-in-program-code.md)。

- 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中打开建模项目及其关系图，然后访问相应内容。 有关详细信息, 请参阅[使用 Visual STUDIO API 打开 UML 模型](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)。

## <a name="see-also"></a>请参阅

- [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)
- [使用 UML API 编程](../modeling/programming-with-the-uml-api.md)
