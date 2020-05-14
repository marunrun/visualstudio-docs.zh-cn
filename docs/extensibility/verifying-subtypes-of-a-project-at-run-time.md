---
title: 在运行时验证项目的子类型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f0d739a9f8734dd8941e3254d03364cbf4c77350
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698172"
---
# <a name="verify-subtypes-of-a-project-at-run-time"></a>在运行时验证项目的子类型
依赖于自定义项目子类型的 VSPackage 应包括用于查找该子类型的逻辑，以便在子类型不存在时，该子类型可以正常失败。 下面的过程演示如何验证是否存在指定的子类型。

### <a name="to-verify-the-presence-of-a-subtype"></a>验证子类型是否存在

1. 通过将以下代码添加到 VSPackage，从项目和解决方案对象<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>中获取项目层次结构作为对象。

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

2. 将层次结构强制转换为<xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected>接口。

    ```csharp
    IVsAggregatableProjectCorrected AP;
    AP = hierarchy as IVsAggregatableProjectCorrected;

    ```

3. 通过调用 获取项目类型 GUID 的列表<xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A>。

    ```csharp
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();

    ```

4. 检查列表以检查指定子类型的 GUID。

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
- [按项目子类型扩展的属性和方法](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)
