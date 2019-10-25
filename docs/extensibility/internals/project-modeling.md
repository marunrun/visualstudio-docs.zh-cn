---
title: 项目建模 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], implementing project objects
- project models, automation
ms.assetid: c8db8fdb-88c1-4b12-86fe-f3c30a18f9ee
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 42e810a36478e49a578c6713d20f1bfc6be98309
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725564"
---
# <a name="project-modeling"></a>项目建模
为项目提供自动化的下一步是实现标准项目对象： <xref:EnvDTE.Projects> 和 `ProjectItems` 集合;`Project` 和 <xref:EnvDTE.ProjectItem> 对象;以及对实现唯一的剩余对象。 这些标准对象在 Dteinternal 文件中定义。 BscPrj 示例中提供了标准对象的实现。 您可以使用这些类作为模型来创建自己的标准项目对象，这些对象与其他项目类型的项目对象并行。

 自动化使用者假定能够调用 <xref:EnvDTE.Solution> （"`<UniqueProjName>")` 和 <xref:EnvDTE.ProjectItems> （`n`），其中 n 是用于获取解决方案中特定项目的索引号。 进行此自动化调用将导致环境在适当的项目层次结构上调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.GetProperty%2A>，并将 VSITEMID_ROOT 作为 ItemID 参数传递，并将 VSHPROPID_ExtObject 作为 VSHPROPID 参数。 `IVsHierarchy::GetProperty` 返回一个 `IDispatch` 指针，该指针指向提供已实现的核心 `Project` 接口的自动化对象。

 下面是 `IVsHierarchy::GetProperty` 的语法。

 `HRESULT GetProperty (`

 `VSITEMID` `itemid`，

 `VSHPROPID` `propid`，

 `VARIANT` `*pvar`

 `);`

 项目可容纳嵌套并使用集合来创建项目项组。 层次结构如下所示。

```
Projects
  |- Project
      |- ProjectItems (a collection of ProjectItem)
          |- ProjectItem (single object) or ProjectItems (another collection)
```

 嵌套意味着 <xref:EnvDTE.ProjectItem> 对象可以同时 <xref:EnvDTE.ProjectItems> 集合，因为 `ProjectItems` 集合可以包含嵌套的对象。 基本项目示例不演示此嵌套。 通过实现 `Project` 对象，您可以参与到类似于树的结构，该结构反映了总体自动化模型的设计。

 项目自动化遵循下图中的路径。

 ![Visual Studio 项目对象](../../extensibility/internals/media/projectobjects.gif "ProjectObjects")项目自动化

 如果未实现 `Project` 对象，环境仍将返回仅包含项目名称的泛型 `Project` 对象。

## <a name="see-also"></a>请参阅
- <xref:EnvDTE.Projects>
- <xref:EnvDTE.ProjectItem>
- <xref:EnvDTE.ProjectItems>