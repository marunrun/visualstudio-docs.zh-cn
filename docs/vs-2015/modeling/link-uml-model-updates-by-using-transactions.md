---
title: 通过使用事务链接 UML 模型更新 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API, transactions
ms.assetid: a1df6c38-a3d1-4a3f-82bc-c8f363ab916e
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f938e08d2bc9363be5e3f9e1ac247dea36f25a80
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191718"
---
# <a name="link-uml-model-updates-by-using-transactions"></a>使用事务链接 UML 模型更新
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在定义扩展到 Visual Studio 中的 UML 设计器时，可以分组到单个事务中调用多项更改*链接的撤消上下文*。 若要查看支持 UML 模式的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
 默认情况下，代码对模型进行的每处修改都可以由用户单独撤销。 例如，如果定义交换两个 UML 类的名称的菜单命令，用户可以调用该命令，然后执行单次撤消。 这将撤消对其中一个名称的更改，但不会撤销对另一个名称的更改，从而让你的模型处于意外状态。  
  
 若要避免此问题，你的代码可以在事务内执行一系列更改。 这就使得一系列更改对用户而言都是单个更改。 随后的撤消命令将撤消整个系列的更改。  
  
 另一个好处是你的代码可以通过引发异常或中止事务撤消一组部分完成的更改。  
  
## <a name="to-group-changes-into-a-single-transaction"></a>将更改分组到单个事务中  
 确保你的项目引用包含该 .NET 程序集：  
  
 **Microsoft.VisualStudio.Modeling.Sdk.[version].dll**  
  
 在你的类内部，声明具有类型 <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ILinkedUndoContext> 的导入属性 ：  
  
 `using Microsoft.VisualStudio.Modeling.ExtensionEnablement;`  
  
 `...`  
  
 `class … {`  
  
 `[Import]`  
  
 `public ILinkedUndoContext LinkedUndoContext { get; set; }`  
  
 在可修改模型的方法中，将你的更改包括到事务中：  
  
 `using (ILinkedUndoTransaction transaction =`  
  
 `LinkedUndoContext.BeginTransaction("my updates"))`  
  
 `{`  
  
 `// code to update model elements or shapes goes here`  
  
 `transaction.Commit();`  
  
 `}`  
  
 注意下列事项：  
  
- 必须始终在事务结束时包括 `Commit()`。 如果在不提交的情况下释放事务，则事务将回滚。 也就是说，该模型将还原到其事务开始时的状态。  
  
- 如果发生在事务内未捕获到的异常，则事务将回滚。 这是一种常见的模式，用于将 `using` 事务块包括到 `try…catch`块中。  
  
- 你可以嵌套事务。  
  
- 你可以向 `BeginTransaction()` 提供任何非空白名称。  
  
- 仅 UML 模型存储区受这些事务影响。 建模事务不会影响：变量、外部存储（如文件和数据库）、层关系图和模型代码。  
  
## <a name="example"></a>示例  
  
```  
    using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
    using Microsoft.VisualStudio.Uml.Interfaces;  
    using Microsoft.VisualStudio.Uml.Classes;  
    using Microsoft.VisualStudio.Uml.Extensions;  
    using System.Linq;  
    using System.ComponentModel.Composition;  
 ...  
  [Import]  
  public ILinkedUndoContext LinkedUndoContext { get; set; }  
  
  /// <summary>  
  /// Swap the names of the currently selected elements.  
  /// </summary>  
  public void Execute(IMenuCommand command)  
  {  
    var selectedShapes =  
      Context.CurrentDiagram.GetSelectedShapes<IClassifier>();  
    if (selectedShapes.Count() < 2) return;  
    IClassifier firstElement = selectedShapes.First().Element;  
    IClassifier lastElement = selectedShapes.Last().Element;  
    string firstName = firstElement.Name;  
    // Perform changes inside a transaction so that undo  
    // works as a single change.  
    using (ILinkedUndoTransaction transaction =   
      LinkedUndoContext.BeginTransaction("Swap names"))  
    {  
        firstElement.Name = lastElement.Name;  
        lastElement.Name = firstName;  
        transaction.Commit();  
    }  
 }  
```  
  
## <a name="see-also"></a>请参阅  
 [使用 UML API 编程](../modeling/programming-with-the-uml-api.md)   
 [在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)
