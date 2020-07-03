---
title: 保持项目项的属性 |Microsoft Docs
ms.date: 03/22/2018
ms.topic: how-to
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 224a1e4f5f5d56022ae7c1e0572ca648b9a5aa6b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85906197"
---
# <a name="persist-the-property-of-a-project-item"></a>保留项目项的属性
你可能希望保留添加到项目项的属性，例如源文件的作者。 可以通过将属性存储在项目文件中来实现此目的。

 将属性保存在项目文件中的第一步是获取作为接口的项目的层次结构 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 。 可以通过使用自动化或使用来获取此接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> 。 获取接口后，可以使用它来确定当前选择的项目项。 获得项目项 ID 后，可以使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> 添加属性。

 在下面的过程中，将*VsPkg.cs*属性 `Author` 与 `Tom` 项目文件中的值保持一致。

## <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>用 DTE 对象获取项目层次结构

1. 将以下代码添加到 VSPackage：

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    ```

## <a name="to-persist-the-project-item-property-with-the-dte-object"></a>用 DTE 对象持久保存项目项属性

1. 将以下代码添加到上一过程的方法中给定的代码：

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

## <a name="to-obtain-the-project-hierarchy-using-ivsmonitorselection"></a>使用 IVsMonitorSelection 获取项目层次结构

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

## <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>如果为，则在给定项目层次结构的情况下保留所选项目项属性

1. 将以下代码添加到上一过程的方法中给定的代码：

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-verify-that-the-property-is-persisted"></a>验证属性是否持久保存

1. 启动 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，然后打开或创建一个解决方案。

2. 在**解决方案资源管理器**中选择项目项 "VsPkg.cs"。

3. 使用断点或以其他方式确定是否已加载 VSPackage 并运行 SetItemAttribute。

   > [!NOTE]
   > 可以在 UI 上下文中 autoload VSPackage <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid> 。 有关详细信息，请参阅[Load vspackage](../extensibility/loading-vspackages.md)。

4. 关闭 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，然后在记事本中打开项目文件。 你应看到 \<Author> 带有值 Tom 的标记，如下所示：

   ```xml
   <Compile Include="VsPkg.cs">
       <Author>Tom</Author>
   </Compile>
   ```

## <a name="see-also"></a>另请参阅

- [自定义工具](../extensibility/internals/custom-tools.md)
