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
ms.openlocfilehash: 11f865a0c39f67b0505a16b209511943756a6981
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328294"
---
# <a name="project-modeling"></a>项目建模
提供的自动化，你的项目实现标准项目对象的下一步：<xref:EnvDTE.Projects>并`ProjectItems`集合;`Project`和<xref:EnvDTE.ProjectItem>对象; 以及对您的实现唯一剩余的对象。 Dteinternal.h 文件中定义这些标准的对象。 BscPrj 示例中提供了标准的对象的一个实现。 可以为模型中使用这些类来创建您自己的标准项目对象，突出显示的-同时与来自其他项目类型的项目对象。

 自动化使用者能够调用将假定<xref:EnvDTE.Solution>("`<UniqueProjName>")`并<xref:EnvDTE.ProjectItems>(`n`) 其中 n 是用于获取解决方案中的特定项目的索引号。 进行此自动化调用会导致环境，以调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.GetProperty%2A>上相应的项目层次结构，将 VSITEMID_ROOT 作为 ItemID 参数和 VSHPROPID_ExtObject 作为 VSHPROPID 参数传递。 `IVsHierarchy::GetProperty` 返回`IDispatch`指针，指向提供核心的自动化对象`Project`接口，该已实现接口。

 下面是语法的`IVsHierarchy::GetProperty`。

 `HRESULT GetProperty (`

 `VSITEMID` `itemid`,

 `VSHPROPID` `propid`,

 `VARIANT` `*pvar`

 `);`

 项目容纳嵌套和使用集合来创建项目项的组。 在层次结构如下所示。

```
Projects
  |- Project
      |- ProjectItems (a collection of ProjectItem)
          |- ProjectItem (single object) or ProjectItems (another collection)
```

 嵌套意味着<xref:EnvDTE.ProjectItem>对象可以是<xref:EnvDTE.ProjectItems>集合中的相同时间处因为`ProjectItems`集合可以包含嵌套的对象。 基本项目示例没有演示这种嵌套模式。 通过实现`Project`对象时，参与整体的自动化模型的设计的特点是类似于树的结构。

 项目自动化遵循下图中的路径。

 ![Visual Studio 项目对象](../../extensibility/internals/media/projectobjects.gif "ProjectObjects")项目自动化

 如果未实现`Project`对象，该环境仍然能够返回泛型`Project`对象，其中包含仅项目的名称。

## <a name="see-also"></a>请参阅
- <xref:EnvDTE.Projects>
- <xref:EnvDTE.ProjectItem>
- <xref:EnvDTE.ProjectItems>