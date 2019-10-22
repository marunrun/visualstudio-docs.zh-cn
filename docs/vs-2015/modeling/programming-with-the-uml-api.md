---
title: 用 UML API 编程 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, API
- UML model, extending
ms.assetid: c5937139-49d0-4439-8a9f-89f5e0474618
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b264987818e244cf016e9b54794109cafc548439
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652099"
---
# <a name="programming-with-the-uml-api"></a>Programming with the UML API
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

利用 Visual Studio 的 UML API，你可以编写代码来创建、读取和更新 UML 模型和关系图。 若要查看支持 UML 模式的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

 下面的主题除了介绍 API 参考页，还介绍了 API。

|主题|描述的示例类型和方法|描述的功能|
|-----------|-----------------------------------------|------------------------|
|[使用 UML API 导航关系](../modeling/navigate-relationships-with-the-uml-api.md)|UML 元素及其属性和关联。 例如，IElement 及其后代，其中包括：IClass、IActivity、IUseCase、IComponent、IInteraction、IModel 和 IPackage|在 Visual Studio 中，UML 模型符合 UML 规范版本2.1.2，可在 " [Uml 资源" 页](http://go.microsoft.com/fwlink/?LinkId=160796)中获取。 每种类型都是一个接口，与 UML 类型具有相同的名称，带有前缀“I”。|
|[在 UML 模型中创建元素和关系](../modeling/create-elements-and-relationships-in-uml-models.md)|IPackage.CreateClass()<br /><br /> IClass.CreateOperation()|每个元素类型都具有创建其子级的方法。|
|[在关系图上显示 UML 模型](../modeling/display-a-uml-model-on-diagrams.md)|IShape、IDiagram<br /><br /> IShape.Move()|模型中的每个元素都可以表示为关系图中的形状。 在某些情况下，可为每个对象创建新形状。 可以对这些形状进行移动、调整大小、着色和折叠或展开。|
|[导航 UML 模型](../modeling/navigate-the-uml-model.md)|IModelStore<br /><br /> IDiagramContext|模型存储区用于存储模型。<br /><br /> 通过关系图上下文，可以访问当前关系图和存储。|
|[使用事务链接 UML 模型更新](../modeling/link-uml-model-updates-by-using-transactions.md)|ILinkedUndoContext|可以将一系列更改链接到一个事务。|
|[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|IMenuCommand<br /><br /> IGestureExtension<br /><br /> ICommandExtension|可通过定义命令（通过双击调用）和拖动到关系图，来扩展关系图的功能。|
|[为 UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)|ValidationContext|可定义有助于确保模型符合指定约束的验证规则。|
|[从 IDataObject 获取 UML 模型元素](../modeling/get-uml-model-elements-from-idataobject.md)|IElement、IShape|当将某个元素从 UML 模型资源管理器或 UML 关系图中拖动到另一个关系图或应用程序时，它将被序列化为 IDataObject。|
|[使用 UML API 编辑 UML 序列图](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md)|IInteraction、ILifeline、IMessage|创建和更新交互图与使用其他类型的关系图稍有不同。|
|[扩展层关系图](../modeling/extend-layer-diagrams.md)|ILayer、ILayerDiagram|可以编写代码来创建和编辑层关系图，同时对照它们来验证程序代码。|

## <a name="about-the-implementation"></a>关于实现
 UML 建模工具是基于 [!INCLUDE[dsl](../includes/dsl-md.md)] 构建的。 每个包和每个关系图都由 [!INCLUDE[dsl](../includes/dsl-md.md)] 模型表示，并有一个规则集合和其他方法来维护它们之间的一致性。

 该平台中的类型在引用的某些程序集中可见，以便编写 UML 扩展。 尽管可以通过访问 [!INCLUDE[dsl](../includes/dsl-md.md)] API 来创建 UML 工具的扩展，但应记住以下注意事项：

- 你可能会发现一些明显十分简单的更改会引发不一致和意外的效果。

- 实现可能在将来更改，这样使用 [!INCLUDE[dsl](../includes/dsl-md.md)] API 所做的改动可能不再有效。

## <a name="the-api-assemblies"></a>API 程序集
 此表总结了为 UML 工具提供扩展性的程序集以及建议使用的命名空间。

|Assembly|命名空间|提供对以下内容的访问：|
|--------------|----------------|-------------------------|
|Microsoft.VisualStudio.Uml.Interfaces|(全部)|UML 类型。|
|Microsoft.VisualStudio.ArchitectureTools.Extensibility|VisualStudio （Microsoft.visualstudio.architecturetools.layer.validator）|[创建方法](../modeling/create-elements-and-relationships-in-uml-models.md)|
||Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation|[关系图和形状](../modeling/display-a-uml-model-on-diagrams.md)|
||Microsoft.VisualStudio.ArchitectureTools.Extensibility|[建模项目](../modeling/read-a-uml-model-in-program-code.md)|
|Microsoft.VisualStudio.Modeling.Sdk.[版本号]|<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement>|[菜单命令扩展](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。<br /><br /> [链接的撤消事务](../modeling/link-uml-model-updates-by-using-transactions.md)。|
||<xref:Microsoft.VisualStudio.Modeling.Validation>|[验证](../modeling/define-validation-constraints-for-uml-models.md)|
||（其他命名空间）|建议仅用于高级用法。|
|Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]|<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement>|[手势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)。|
||（其他命名空间）|建议仅用于高级用法。|
|Microsoft.VisualStudio.TeamFoundation.WorkItemTracking|Microsoft.VisualStudio.TeamFoundation.WorkItemTracking|指向[工作项的链接](../modeling/define-a-work-item-link-handler.md)。|
|Microsoft.TeamFoundation.WorkItemTracking.Client|Microsoft.TeamFoundation.WorkItemTracking.Client|[工作项及其字段](../modeling/define-a-work-item-link-handler.md)。|
|Microsoft.TeamFoundation.Client|Microsoft.TeamFoundation.Client|[工作项及其字段](../modeling/define-a-work-item-link-handler.md)。|
|System.ComponentModel.Composition|<xref:System.ComponentModel.Composition>|[MEF 组件的导出和导入](../modeling/define-and-install-a-modeling-extension.md)|
|System.Linq|<xref:System.Linq>|[简单地操作集合，尤其是在处理关系时](../modeling/navigate-relationships-with-the-uml-api.md)。|

## <a name="see-also"></a>请参阅
 [扩展 uml 模型和关系图](../modeling/extend-uml-models-and-diagrams.md) [API 参考以实现 uml 建模扩展性](../modeling/api-reference-for-uml-modeling-extensibility.md)
