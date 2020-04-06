---
title: 项目建模 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], implementing project objects
- project models, automation
ms.assetid: c8db8fdb-88c1-4b12-86fe-f3c30a18f9ee
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c1ac89baf5bc7582d3430532938a5e5a0c35a4c0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706544"
---
# <a name="project-modeling"></a>项目建模
为项目提供自动化的下一步是实现标准项目对象：<xref:EnvDTE.Projects>和`ProjectItems`集合;`Project`和<xref:EnvDTE.ProjectItem>对象;以及实现所特有的其余对象。 这些标准对象在 Dtein.h 文件中定义。 BscPrj 示例提供了标准对象的实现。 可以将这些类用作模型，以创建与来自其他项目类型的项目对象并排站在一起的标准项目对象。

 自动化使用者<xref:EnvDTE.Solution>假定能够调用 （"`<UniqueProjName>")`和<xref:EnvDTE.ProjectItems>）`n`，其中 n 是获取解决方案中特定项目的索引号。 进行此自动化调用会导致环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.GetProperty%2A>相应的项目层次结构，将VSITEMID_ROOT作为 ItemID 参数传递，并将VSHPROPID_ExtObject作为 VSHPROPID 参数。 `IVsHierarchy::GetProperty`返回指向`IDispatch`提供核心`Project`接口的自动化对象的指针，该接口已实现。

 下面是`IVsHierarchy::GetProperty`的语法。

 `HRESULT GetProperty (`

 `VSITEMID` `itemid`,

 `VSHPROPID` `propid`,

 `VARIANT` `*pvar`

 `);`

 项目容纳嵌套并使用集合创建项目项组。 层次结构如下所示。

```
Projects
  |- Project
      |- ProjectItems (a collection of ProjectItem)
          |- ProjectItem (single object) or ProjectItems (another collection)
```

 嵌套意味着<xref:EnvDTE.ProjectItem>可以同时<xref:EnvDTE.ProjectItems>收集对象，因为`ProjectItems`集合可以包含嵌套对象。 基本项目示例不演示此嵌套。 通过实现对象`Project`，您可以参与整个自动化模型设计的特征树状结构。

 项目自动化遵循下图中的路径。

 ![可视化工作室项目对象](../../extensibility/internals/media/projectobjects.gif "ProjectObjects")项目自动化

 如果不实现`Project`对象，环境仍将返回仅包含项目名称的泛型`Project`对象。

## <a name="see-also"></a>请参阅
- <xref:EnvDTE.Projects>
- <xref:EnvDTE.ProjectItem>
- <xref:EnvDTE.ProjectItems>
