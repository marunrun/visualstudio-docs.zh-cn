---
title: 保存项目项的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4adcf0f5c5770f5d3ffc0e0ed9bffdb108869c7f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441548"
---
# <a name="persisting-the-property-of-a-project-item"></a>保留项目项的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可能想要保留的属性添加到项目项，例如源代码文件的作者。 可以通过将属性存储在项目文件中执行此操作。  
  
 若要保存项目文件中的属性的第一步是获取作为项目的层次结构<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>接口。 你可以通过使用自动化功能或通过使用获取此接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>。 一旦获取该接口，可用于确定当前未选择的项目项。 项目项 ID 后，可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A>添加属性。  
  
 在以下过程中，保留 VsPkg.cs 属性`Author`具有值`Tom`项目文件中。  
  
### <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>若要获取 DTE 对象使用的项目层次结构  
  
1. 将以下代码添加到你的 VSPackage 中：  
  
    ```csharp  
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));  
    EnvDTE.Project project = dte.Solution.Projects.Item(1);  
  
    string uniqueName = project.UniqueName;  
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));  
    IVsHierarchy hierarchy;  
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);  
    ```  
  
### <a name="to-persist-the-project-item-property-with-the-dte-object"></a>若要保存项目项属性与 DTE 对象  
  
1. 将以下代码添加到在上一个过程中的方法中提供的代码：  
  
    ```csharp  
    IVsBuildPropertyStorage buildPropertyStorage =   
        hierarchy as IVsBuildPropertyStorage;  
    if (buildPropertyStorage != null)  
    {  
        uint itemId;  
        string fullPath = (string)project.ProjectItems.Item(  
            "VsPkg.cs").Properties.Item("FullPath").Value;  
        hierarchy.ParseCanonicalName(fullPath, out itemId);  
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");  
    }  
    ```  
  
### <a name="to-obtain-the-project-hierarchy-using-ivsmonitorselection"></a>若要获取使用 IVsMonitorSelection 的项目层次结构  
  
1. 将以下代码添加到你的 VSPackage 中：  
  
    ```csharp  
    IVsHierarchy hierarchy = null;  
    IntPtr hierarchyPtr = IntPtr.Zero;  
    IntPtr selectionContainer = IntPtr.Zero;  
    uint itemid;  
  
    // Retrieve shell interface in order to get current selection  
    IVsMonitorSelection monitorSelection =     Package.GetGlobalService(typeof(SVsShellMonitorSelection)) as     IVsMonitorSelection;  
    if (monitorSelection == null)  
        throw new InvalidOperationException();  
  
    try  
    {  
        // Get the current project hierarchy, project item, and selection container for the current selection  
        // If the selection spans multiple hierachies, hierarchyPtr is Zero  
        IVsMultiItemSelect multiItemSelect = null;  
        ErrorHandler.ThrowOnFailure(  
            monitorSelection.GetCurrentSelection(  
                out hierarchyPtr, out itemid,   
                out multiItemSelect, out selectionContainer));  
  
        // We only care if there is only one node selected in the tree  
        if (!(itemid == VSConstants.VSITEMID_NIL ||   
            hierarchyPtr == IntPtr.Zero ||  
            multiItemSelect != null ||  
            itemid == VSConstants.VSITEMID_SELECTION))  
        {  
            hierarchy = Marshal.GetObjectForIUnknown(hierarchyPtr)  
                as IVsHierarchy;  
        }  
    }  
    finally  
    {  
        if (hierarchyPtr != IntPtr.Zero)  
            Marshal.Release(hierarchyPtr);  
        if (selectionContainer != IntPtr.Zero)  
            Marshal.Release(selectionContainer);  
    }  
    ```  
  
2. 
  
### <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>若要保留选定的项目项属性，给定的项目层次结构  
  
1. 将以下代码添加到在上一个过程中的方法中提供的代码：  
  
    ```  
    IVsBuildPropertyStorage buildPropertyStorage =   
        hierarchy as IVsBuildPropertyStorage;  
    if (buildPropertyStorage != null)  
    {  
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");  
    }  
    ```  
  
### <a name="to-verify-that-the-property-is-persisted"></a>若要验证属性保持不变  
  
1. 启动[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]然后打开或创建解决方案。  
  
2. 选择的项目项中的 VsPkg.cs**解决方案资源管理器**。  
  
3. 使用断点或否则来确定加载你的 VSPackage 和 SetItemAttribute 运行。  
  
    > [!NOTE]
    > 你可以自动加载 VSPackage 的 UI 上下文中<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>。 有关详细信息，请参阅[加载 Vspackage](../extensibility/loading-vspackages.md)。  
  
4. 关闭[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，然后在记事本中打开项目文件。 应会看到\<作者 > 标记值 Tom，按如下所示：  
  
    ```  
    <Compile Include="VsPkg.cs">  
        <Author>Tom</Author>  
    </Compile>  
    ```  
  
## <a name="see-also"></a>请参阅  
 [自定义工具](../extensibility/internals/custom-tools.md)
