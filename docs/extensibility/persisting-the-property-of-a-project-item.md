---
title: 保留项目项的属性 |微软文档
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 15c280f15436a5e27bcc0dcc4d2fb9e9bdd82933
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702210"
---
# <a name="persist-the-property-of-a-project-item"></a>保留项目项的属性
您可能希望保留添加到项目项的属性，例如源文件的作者。 可以通过将属性存储在项目文件中来执行此操作。

 在项目文件中保留属性的第一步是获取项目的层次结构作为<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>接口。 您可以使用 自动化或使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>获取此接口。 获取接口后，可以使用它确定当前选择了哪个项目项。 获得项目项 ID 后，可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A>添加 属性。

 在以下过程中，您将*VsPkg.cs*属性`Author`与项目文件中的值`Tom`保持一起。

## <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>使用 DTE 对象获取项目层次结构

1. 将以下代码添加到 VSPackage：

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    ```

## <a name="to-persist-the-project-item-property-with-the-dte-object"></a>使用 DTE 对象保留项目项属性

1. 将以下代码添加到前面的过程中方法中给出的代码：

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

## <a name="to-obtain-the-project-hierarchy-using-ivsmonitorselection"></a>使用 IVsMonitor 选择获取项目层次结构

1. 将以下代码添加到 VSPackage：

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

## <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>要保留选定的项目项属性，给定项目层次结构

1. 将以下代码添加到前面的过程中方法中给出的代码：

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-verify-that-the-property-is-persisted"></a>验证属性是否持久化

1. 启动[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，然后打开或创建解决方案。

2. 在**解决方案资源管理器**中选择项目项VsPkg.cs。

3. 使用断点或以其他方式确定您的 VS 包已加载，并且 SetItem属性运行。

   > [!NOTE]
   > 您可以在 UI 上下文中<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>自动加载 VSPackage。 有关详细信息，请参阅加载[VS 包](../extensibility/loading-vspackages.md)。

4. 关闭[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，然后在记事本中打开项目文件。 您应该会看到带有"Tom"值的\<"作者>"标记，如下所示：

   ```xml
   <Compile Include="VsPkg.cs">
       <Author>Tom</Author>
   </Compile>
   ```

## <a name="see-also"></a>请参阅

- [自定义工具](../extensibility/internals/custom-tools.md)
