---
title: 与 UML API 导航关系 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API
ms.assetid: a4d11d45-b8c0-40f9-a597-363f07659610
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 74a8234dfc38ef5ef41cd77b2ce10eaf54018622
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850093"
---
# <a name="navigate-relationships-with-the-uml-api"></a>使用 UML API 导航关系
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含按不同类型的关系链接在一起的元素的模型。 本主题介绍如何在程序代码中导航模型。

## <a name="traversing-relationships"></a>遍历关系

### <a name="any-relationship"></a>任何关系
 使用 `GetRelatedElements<T>()` 查找连接到指定元素的所有元素。 将 `T` 设置为 `IRelationship` 以遍历所有类型的关系，或使用更具体的类型（如 `IAssociation` 以便仅遍历此类型。

```
IElement anElement;
// Select all elements related to anElement.
Context.CurrentDiagram.SelectShapes (
   anElement.GetRelatedElements<IRelationship>()
    .SelectMany(e=>e.Shapes()).ToArray());

```

 使用 `GetRelatedLinks<T>()` 查找连接到某个元素的所有关系。

```
// Process all relationships connected to an element.
foreach (IRelationship relationship in
   anElement.GetRelatedLinks<IRelationship>())
{
  Debug.Assert(relationship.SourceElement == anElement
      || relationship.TargetElement == anElement);
}

```

### <a name="association"></a>关联
 关联是指两个属性之间的关系，其中每个属性均属于一个分类器。

```
IClassifier classifier; // class, interface, component, actor, ...
// Get all the associations sourced from this classifier
foreach (IProperty p in classifier.GetOutgoingAssociationEnds())
{
  // p represents the end further end of an association.
  IType oppositeElement = p.Type;
    // The type to which this association connects classifier

  IProperty oppositeProperty = p.Opposite;
    // The nearer end of the association.
  Debug.Assert(oppositeProperty.Type == classifier);
  IAssociation association = p.Association;
  Debug.Assert(association.MemberEnds.Contains(p)
     && association.MemberEnds.Contains(oppositeProperty));
}
```

### <a name="generalization-and-realization"></a>泛化和实现
 访问泛化的另一端：

```
foreach (IClassifier supertype in classifier.Generals) {…}
foreach (IClassifier subtype in classifier.GetSpecifics()) {…}
Access the relationship itself:
foreach (IGeneralization gen in classifier.Generalizations)
{ Debug.Assert(classifier == gen.Specific); }
```

```

/// InterfaceRealization:
IEnumerable<IInterface> GetRealizedInterfaces
    (this IBehavioredClassifier classifier);
IEnumerable<IBehavioredClassifier> GetRealizingClassifiers
    (this IInterface interface);

```

### <a name="dependency"></a>依赖关系

```
/// Returns the elements depending on this element
IEnumerable<INamedElement> GetDependencyClients(this INamedElement element);
/// Returns the elements this element depends on
IEnumerable<INamedElement> INamedElement GetDependencySuppliers(this INamedElement element);

```

### <a name="activity-edge"></a>活动边缘

```
/// Returns the nodes targeted by edges outgoing from this one
IEnumerable<IActivityNode> GetActivityEdgeTargets(this IActivityNode node);
/// Returns the nodes sourcing edges incoming to this one
IEnumerable<IActivityNode> GetActivityEdgeSources(this IActivityNode node);

```

### <a name="connector-assembly-and-delegation"></a>连接器（程序集和委派）

```
/// Returns the elements connected via assembly
/// or delegation to this one
IEnumerable<IConnectableElement> GetConnectedElements(this IConnectableElement element);

```

### <a name="messages-and-lifelines"></a>消息和生命线

```
IEnumerable<IMessage> GetAllOutgoingMessages(this ILifeline  lifeline);
// both from lifeline and execution occurrences
IEnumerable<IMessage> GetAllIncomingMessages(this ILifeline  lifeline);
ILifeline GetSourceLifeline(this IMessage message);
    // may return null for found messages
ILifeline GetTargetLifeline(this IMessage message);
    // may return null for lost messages

```

### <a name="package-import"></a>包导入

```
IEnumerable<IPackage>GetImportedPackages(this INamespace namespace);
IEnumerable<INamespace> GetImportingNamespaces(this IPackage package);

```

### <a name="use-case-extend-and-include"></a>用例扩展和包含

```
IEnumerable<IUseCase>GetExtendedCases(this IUseCase usecase);
IEnumerable<IUseCase>GetExtendingCases(this IUseCase usecase);
IEnumerable<IUseCase>GetIncludedCases(this IUseCase usecase);
IEnumerable<IUseCase>GetIncludingCases(this IUseCase usecase);
```

## <a name="enumerating-relationships"></a>枚举关系
 返回多个值的 UML 模型的所有属性都符合 IEnumerable < > 接口。 这意味着你可以使用[Linq 查询表达式](https://docs.microsoft.com/dotnet/csharp/linq/index)和在**system.web**命名空间中定义的扩展方法。

 例如：

```
from shape in     Context.CurrentDiagram.GetSelectedShapes<IClassifier>()
where shape.Color == System.Drawing.Color.Red
select shape.Element

```

## <a name="see-also"></a>请参阅
 [扩展 uml 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)[导航 uml 模型](../modeling/navigate-the-uml-model.md)
