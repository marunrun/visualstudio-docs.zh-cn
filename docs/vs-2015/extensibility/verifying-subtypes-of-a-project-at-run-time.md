---
title: 在运行时验证项目的子类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1e3940097ac53255b7bdd2c12c9ccc64605016e1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62584900"
---
# <a name="verifying-subtypes-of-a-project-at-run-time"></a>在运行时验证项目的子类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

依赖于自定义项目子类型的 VSPackage 应该包含用于查找子类型的逻辑，以便在子类型不存在时可以正常失败。 下面的过程演示如何验证是否存在指定的子类型。  
  
### <a name="to-verify-the-presence-of-a-subtype"></a>验证子类型是否存在  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>通过将以下代码添加到 VSPackage，从项目和解决方案对象获取项目层次结构作为对象。  
  
    ```  
    EnvDTE.DTE dte;  
    dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));  
  
    EnvDTE.Project project;  
    project = dte.Solution.Projects.Item(1);  
  
    IVsSolution solution;  
    solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));  
  
    IVsHierarchy hierarchy;  
    hierarchy = solution.GetProjectOfUniqueName(project.UniqueName);  
  
    ```  
  
2. 将层次结构强制转换为 <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected> 接口。  
  
    ```  
    IVsAggregatableProjectCorrected AP;  
    AP = hierarchy as IVsAggregatableProjectCorrected;  
  
    ```  
  
3. 通过调用获取项目类型 Guid 的列表 <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A> 。  
  
    ```  
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();  
  
    ```  
  
4. 检查列表中是否有指定子类型的 GUID。  
  
    ```  
    // Replace the string "MyGUID" with the GUID of the subtype.  
    string guidMySubtype = "MyGUID";  
    if (projTypeGuids.IndexOf(guidMySubtype) > 0)  
    {  
        // The specified subtype is present.  
    }  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [项目子类型](../extensibility/internals/project-subtypes.md)   
 [项目子类型设计](../extensibility/internals/project-subtypes-design.md)   
 [项目子类型扩展的属性和方法](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)
