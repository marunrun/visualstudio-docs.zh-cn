---
title: 在运行时验证项目的子类型 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 033f2971d0b8acb0390765f240a86a5ff543c353
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310692"
---
# <a name="verify-subtypes-of-a-project-at-run-time"></a>在运行时验证项目的子类型
取决于自定义项目子类型的 VSPackage 应包括逻辑来查找子类型，以便它可以正常退出如果相应的子类型不存在。 以下过程说明如何验证存在指定的子类型。

### <a name="to-verify-the-presence-of-a-subtype"></a>若要验证存在子类型

1. 从为项目和解决方案对象中获取的项目层次结构<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>通过将以下代码添加到你的 VSPackage 的对象。

    ```csharp
    EnvDTE.DTE dte;
    dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));

    EnvDTE.Project project;
    project = dte.Solution.Projects.Item(1);

    IVsSolution solution;
    solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));

    IVsHierarchy hierarchy;
    hierarchy = solution.GetProjectOfUniqueName(project.UniqueName);

    ```

2. 强制转换为层次结构<xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected>接口。

    ```csharp
    IVsAggregatableProjectCorrected AP;
    AP = hierarchy as IVsAggregatableProjectCorrected;

    ```

3. 通过调用获取的项目类型 Guid 列表<xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A>。

    ```csharp
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();

    ```

4. 检查指定的子类型的 GUID 的列表。

    ```csharp
    // Replace the string "MyGUID" with the GUID of the subtype.
    string guidMySubtype = "MyGUID";
    if (projTypeGuids.IndexOf(guidMySubtype) > 0)
    {
        // The specified subtype is present.
    }
    ```

## <a name="see-also"></a>请参阅
- [项目子类型](../extensibility/internals/project-subtypes.md)
- [项目子类型设计](../extensibility/internals/project-subtypes-design.md)
- [属性和方法由项目子类型扩展](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)