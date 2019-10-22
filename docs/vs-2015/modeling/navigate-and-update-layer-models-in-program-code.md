---
title: 在程序代码中导航和更新层模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer models, navigating in program code
- layer models, updating in program code
ms.assetid: c60edc87-33ee-4964-a954-40069f9febf3
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 88ab52f1b06e6a2da94d17225bdb26ecec358a6c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668572"
---
# <a name="navigate-and-update-layer-models-in-program-code"></a>在程序代码中导航和更新层模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍了层模型中的元素和关系，可使用程序代码进行导航和更新。 有关从用户角度来看层关系图的详细信息，请参阅[层关系图：参考](../modeling/layer-diagrams-reference.md)层关系图和[层关系图：准则](../modeling/layer-diagrams-guidelines.md)。

 本主题中描述的 `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer` 模型是更通用 <xref:Microsoft.VisualStudio.GraphModel> 模型的外观。 如果要编写[菜单命令或笔势扩展](../modeling/add-commands-and-gestures-to-layer-diagrams.md)，请使用 `Layer` 模型。 如果你正在编写[层验证扩展](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)，则使用 `GraphModel` 会更容易。

## <a name="transactions"></a>事务
 更新模型时，请考虑将更改包含在一个 `ILinkedUndoTransaction` 中。 这会将你所做的更改分组到一个事务。 如果有任何更改失败，则将回滚整个事务。 如果用户撤消一个更改，将一起撤消所有更改。

 有关详细信息，请参阅[使用事务链接 UML 模型更新](../modeling/link-uml-model-updates-by-using-transactions.md)。

```
using (ILinkedUndoTransaction t =
        LinkedUndoContext.BeginTransaction("a name"))
{
    // Make changes here ....
    t.Commit(); // Don't forget this!
}
```

## <a name="containment"></a>包含
 ![ILayer 和 ILayerModel 均可包含 ILayers。](../modeling/media/layerapi-containment.png "LayerApi_Containment")

 层（[ILayer](/previous-versions/ff644251(v=vs.140))）和层模型（[ILayerModel](/previous-versions/ff643069(v=vs.140))）可以包含注释和层。

 层 (`ILayer`) 可以包含在层模型 (`ILayerModel`) 中，也可以嵌套在另一个 `ILayer` 中。

 若要创建注释或层，则对相应容器使用创建方法。

## <a name="dependency-links"></a>依赖关系链接
 依赖关系链接由一个对象表示。 可以在任一方向导航链接：

 ![ILayerDependencyLink 连接两个 ILayers。](../modeling/media/layerapi-dependency.png "LayerApi_Dependency")

 若要创建依赖关系链接，请调用 `source.CreateDependencyLink(target)`。

## <a name="comments"></a>注释
 注释可以包含在层或层模型内部，也可以链接到任何层元素：

 ![可以将注释附加到任何层元素。](../modeling/media/layerapi-comments.png "LayerApi_Comments")

 注释可以链接到任意数量的元素，也可以不链接任何元素。

 若要获取附加到层元素的注释，请使用：

```csharp
ILayerModel model = diagram.GetLayerModel();
IEnumerable<ILayerComment> comments =
   model.Comments.Where(comment =>
      comment.Links.Any(link => link.Target == layerElement));

```

> [!CAUTION]
> `Comments` 的 `ILayer` 属性可获取包含在 `ILayer` 内的注释。 但不会获取链接到它的注释。

 通过对相应容器调用 `CreateComment()` 来创建注释。

 通过对注释使用 `CreateLink()` 来创建链接。

## <a name="layer-elements"></a>层元素
 可包含在一个模型中的所有类型的元素都是层元素：

 ![层关系图内容为 ILayerElements。](../modeling/media/layerapi-layerelements.png "LayerApi_LayerElements")

## <a name="properties"></a>属性
 每个 `ILayerElement` 都有一个名为 `Properties` 的字符串字典。 可以使用此字典将任意信息附加到任何层元素。

## <a name="artifact-references"></a>项目引用
 项目引用（[ILayerArtifactReference](/previous-versions/ff644536(v=vs.140))）表示层和项目项（如文件、类或文件夹）之间的链接。 当用户通过将项从解决方案资源管理器、类视图或对象浏览器中拖动到层关系图中来创建层或向其进行添加时，将创建项目。 可将任意数量的项目引用链接到一个层。

 “层资源管理器”中的每一行都显示一个项目引用。 有关详细信息，请参阅[从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)。

 下面是与项目引用有关的主要类型和方法：

 [ILayerArtifactReference](/previous-versions/ff644536(v=vs.140))。 Categories 属性指示引用的项目类型，例如类、可执行文件或程序集。 Categories 确定标识符标识目标项目的方式。

 [ArtifactReferenceExtensions](/previous-versions/ff695840(v=vs.140))从 <xref:EnvDTE.Project> 或 <xref:EnvDTE.ProjectItem> 创建项目引用。 这是一个异步操作。 因此，你通常要提供一个在创建操作完成时调用的回调。

 层项目引用不应与用例关系图中的项目混淆。

## <a name="shapes-and-diagrams"></a>形状和关系图
 两个对象用于表示层模型中的每个元素：一个 `ILayerElement` 和一个[IShape](/previous-versions/ee806673(v=vs.140))。 `IShape` 表示关系图上形状的位置和大小。 在层模型中，每个 `ILayerElement` 都有一个 `IShape`，层关系图上的每个 `IShape` 都有一个 `ILayerElement`。 `IShape` 还用于 UML 模型。 因此，并不是每一个 `IShape` 都具有层元素。

 同样，`ILayerModel` 将显示在一个[IDiagram](/previous-versions/ee789658(v=vs.140))上。

 在自定义命令或笔势处理程序的代码中，你可以从 `DiagramContext` 导入中获取当前关系图和当前选择的形状：

```
public class ... {
[Import]
    public IDiagramContext DiagramContext { get; set; }
...
public void ... (...)
{ IDiagram diagram = this.DiagramContext.CurrentDiagram;
  ILayerModel model = diagram.GetLayerModel();
  if (model != null)
  { foreach (ILayer layer in model.Layers) { ... }}
  foreach (IShape selected in diagram.SelectedShapes)
  { ILayerElement element = selected.GetLayerElement();
    if (element != null) ... }}
```

 ![每个 ILayerElement 都由一个 IShape 表示。](../modeling/media/layerapi-shapes.png)

 [IShape](/previous-versions/ee806673(v=vs.140))和[IDiagram](/previous-versions/ee789658(v=vs.140))还用于显示 UML 模型。 有关详细信息，请参阅[在关系图上显示 UML 模型](../modeling/display-a-uml-model-on-diagrams.md)。

## <a name="see-also"></a>请参阅

- [向层关系图添加命令和笔势](../modeling/add-commands-and-gestures-to-layer-diagrams.md)
- [向层关系图添加自定义体系结构验证](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)
- [向层关系图添加自定义属性](../modeling/add-custom-properties-to-layer-diagrams.md)
- [层关系图：参考](../modeling/layer-diagrams-reference.md)
- [层关系图：指南](../modeling/layer-diagrams-guidelines.md)
- [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)
