---
title: 在 UML 模型中创建元素和关系 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API
ms.assetid: cae81d32-8cc7-4f7c-9f00-20119952bc51
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ce1f236347ad811f1c5d115f30907b7e3356e3af
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68159636"
---
# <a name="create-elements-and-relationships-in-uml-models"></a>在 UML 模型中创建元素和关系
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可在 Visual Studio 扩展的程序代码中创建和删除元素和关系。  
  
## <a name="create-a-model-element"></a>创建模型元素  
  
### <a name="namespace-imports"></a>命名空间导入  
 必须包括以下 `using` 语句。  
  
 创建方法被定义为此命名空间中的扩展方法：  
  
 `using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;`  
  
### <a name="obtain-the-owner-of-the-element-you-want-to-create"></a>获取需要创建的元素的所有者  
 模型构成单个树，以便每项都有一个所有者，但模型根除外。 模型根属于 `IModel` 类型，这是 `IPackage` 的一种类型。  
  
 如果要创建将在特定关系图（比如用户的当前关系图）中显示的元素，通常应在链接到该关系图的包中进行创建。 例如：  
  
```  
IPackage linkedPackage = Context.CurrentDiagram.Element as IPackage;  
```  
  
 此表总结了常见模型元素的所有权：  
  
|要创建的元素|Owner|  
|---------------------------|-----------|  
|`IActor, IUseCase, IComponent, IClass, IInterface, IEnumeration`<br /><br /> `IActivity, IInteraction`|`IPackage, IModel`|  
|`IAttribute, IOperation`|`IClass, IInterface`|  
|`IPart, IPort`|`IComponent`|  
|`IAction, IObjectNode`|`IActivity`|  
|`ILifeline, IMessage, ICombinedFragment`|`IInteraction`|  
  
### <a name="invoke-the-create-method-on-the-owner"></a>对所有者调用 Create 方法  
 方法名称的形式：`Create`*OwnedType*`()`。 例如:  
  
```  
IUseCase usecase1 = linkedPackage.CreateUseCase();  
```  
  
 某些类型具有更复杂的创建方法，尤其是在序列图中。 请参阅[通过使用 UML API 编辑 UML 序列图](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md)。  
  
 对于某些类型的元素，可以使用 `SetOwner(newOwner)` 在其生存期内更改元素的所有者。  
  
### <a name="set-the-name-and-other-properties"></a>设置名称和其他属性  
  
```  
usecase1.Name = "user logs in";  
```  
  
### <a name="example"></a>示例  
  
```  
using Microsoft.VisualStudio.Uml.Classes;  
using Microsoft.VisualStudio.Uml.Extensions;  
...  
 void InstantiateObserverPattern (IPackage package, string namePrefix)  
 {    IInterface observer = package.CreateInterface();  
      observer.Name = namePrefix + "Observer";  
      IOperation operation = observer.CreateOperation();  
      operation.Name = "Update";  
      IClass subject = package.CreateClass();  
      subject.Name = namePrefix + "Subject"; ...  
```  
  
## <a name="create-an-association"></a>创建关联  
  
#### <a name="to-create-an-association"></a>创建关联  
  
1. 获取关联的所有者，它通常是包含关系源端的包或模型。  
  
2. 对所有者调用所需的 Create 方法。  
  
3. 设置关系的属性，比如其名称。  
  
     例如：  
  
    ```  
    IAssociation association = subject.Package.CreateAssociation(subject, observer);  
    association .Name = "Observes";  
    ```  
  
4. 设置关系各端的属性。 始终有两个 `MemberEnds`。 例如:  
  
    ```  
    association .MemberEnds[0].Name = "subject";   // role name  
    association .MemberEnds[1].Name = "observers"; // role name  
    association .MemberEnds[1].SetBounds("0..*");           
                // multiplicity defaults to "1"  
    association.MemberEnds[0].Aggregation = AggregationKind.Composite;  
    ```  
  
## <a name="create-a-generalization"></a>创建泛化  
  
```  
IGeneralization generalization =   
  subclass.CreateGeneralization(superClass);  
```  
  
## <a name="delete-an-element-relationship-or-generalization-from-the-model"></a>从模型中删除元素、关系或泛化  
  
```  
anElement.Delete();  
```  
  
 从模型中删除元素时：  
  
- 也将删除链接到它的每个关系。  
  
- 还将删除关系图上表示它的每个形状。  
  
## <a name="see-also"></a>请参阅  
 [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)   
 [在关系图上显示 UML 模型](../modeling/display-a-uml-model-on-diagrams.md)
