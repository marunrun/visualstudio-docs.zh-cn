---
title: 管理通用 Windows 项目 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 47926aa1-3b41-410d-bca8-f77fc950cbe7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e542d1cc53fbdfb287d004c15b2a9055d3a0cba1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72647946"
---
# <a name="manage-universal-windows-projects"></a>管理通用 Windows 项目

通用 Windows 应用是面向 Windows 8.1 和 Windows Phone 8.1 的应用，使开发人员能够在这两个平台上使用代码和其他资产。 共享代码和资源保留在共享项目中，而特定于平台的代码和资源保留在单独的项目中，一个用于 Windows，另一个用于 Windows Phone。 有关通用 Windows 应用的详细信息，请参阅[通用 windows 应用](https://msdn.microsoft.com/library/windows/apps/dn609832.aspx)。 用于管理项目的 Visual Studio 扩展应该知道，通用 Windows 应用程序项目的结构与单平台应用程序不同。 本演练演示如何导航共享项目并管理共享项。

## <a name="prerequisites"></a>Prerequisites

从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="navigate-the-shared-project"></a>导航共享项目

1. 创建名C#为**TestUniversalProject**的 VSIX 项目。 （**文件** > **新**的  > **项目**， **C#** 然后  > **扩展性** > **Visual Studio 包**中）。 添加**自定义命令**项目项模板（在**解决方案资源管理器**上，右键单击项目节点，然后选择 "**添加** > **新项**"，然后单击 "**扩展性**"。 将该文件命名为**TestUniversalProject**。

2. 添加对 VisualStudio 和*DesignTime*的引用（在 "扩展" 部分*中，为*"**扩展名**" 部分），然后添加一个。

3. 打开*TestUniversalProject.cs*并添加以下 `using` 指令：

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.PlatformUI;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using System.Collections.Generic;
    using System.IO;
    using System.Windows.Forms;
    ```

4. 在 `TestUniversalProject` 类中，添加指向 "**输出**" 窗口的私有字段。

    ```csharp
    public sealed class TestUniversalProject
    {
        IVsOutputWindowPane output;
    . . .
    }
    ```

5. 将引用设置为 TestUniversalProject 构造函数中的 "输出" 窗格：

    ```csharp
    private TestUniversalProject(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);
            EventHandler eventHandler = this.ShowMessageBox;
            MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);
            commandService.AddCommand(menuItem);
        }
        // get a reference to the Output window
                    output = (IVsOutputWindowPane)ServiceProvider.GetService(typeof(SVsGeneralOutputWindowPane));
    }
    ```

6. 删除 `ShowMessageBox` 方法中的现有代码：

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
    }
    ```

7. 获取 DTE 对象，在本演练中，我们将使用这些对象进行多种不同的目的。 此外，请确保在单击菜单按钮时加载解决方案。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (EnvDTE.DTE)this.ServiceProvider.GetService(typeof(EnvDTE.DTE));
        if (dte.Solution != null)
        {
            . . .
        }
        else
        {
            MessageBox.Show("No solution is open");
            return;
        }
    }
    ```

8. 查找共享项目。 共享项目是一个纯容器;它不生成或生成输出。 下面的方法通过查找具有共享项目功能的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 对象查找解决方案中的第一个共享项目。

    ```csharp
    private IVsHierarchy FindSharedProject()
    {
        var sln = (IVsSolution)this.ServiceProvider.GetService(typeof(SVsSolution));
        Guid empty = Guid.Empty;
        IEnumHierarchies enumHiers;

        //get all the projects in the solution
        ErrorHandler.ThrowOnFailure(sln.GetProjectEnum((uint)__VSENUMPROJFLAGS.EPF_LOADEDINSOLUTION, ref empty, out enumHiers));
        foreach (IVsHierarchy hier in ComUtilities.EnumerableFrom(enumHiers))
        {
            if (PackageUtilities.IsCapabilityMatch(hier, "SharedAssetsProject"))
            {
                return hier;
            }
        }
        return null;
    }
    ```

9. 在 `ShowMessageBox` 方法中，输出共享项目的标题（出现在**解决方案资源管理器**中的项目名称）。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));

        if (dte.Solution != null)
        {
            var sharedHier = this.FindSharedProject();
            if (sharedHier != null)
            {
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,
                     (int)__VSHPROPID.VSHPROPID_Caption);
                output.OutputStringThreadSafe(string.Format("Found shared project: {0}\n", sharedCaption));
            }
            else
            {
                MessageBox.Show("Solution has no shared project");
                return;
            }
                }
        else
        {
            MessageBox.Show("No solution is open");
            return;
        }
    }
    ```

10. 获取活动平台项目。 平台项目是包含特定于平台的代码和资源的项目。 下面的方法使用新的字段 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy> 获取活动平台项目。

    ```csharp
    private IVsHierarchy GetActiveProjectContext(IVsHierarchy hierarchy)
    {
        IVsHierarchy activeProjectContext;
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,
             (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, out activeProjectContext))
        {
            return activeProjectContext;
        }
        else
        {
            return null;
        }
    }
    ```

11. 在 `ShowMessageBox` 方法中，输出活动平台项目的标题。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));

        if (dte.Solution != null)
        {
            var sharedHier = this.FindSharedProject();
            if (sharedHier != null)
            {
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,
                     (int)__VSHPROPID.VSHPROPID_Caption);
                output.OutputStringThreadSafe(string.Format("Shared project: {0}\n", sharedCaption));

                var activePlatformHier = this.GetActiveProjectContext(sharedHier);
                if (activePlatformHier != null)
                {
                    string activeCaption = HierarchyUtilities.GetHierarchyProperty<string>(activePlatformHier,
                         (uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID.VSHPROPID_Caption);
                    output.OutputStringThreadSafe(string.Format("Active platform project: {0}\n", activeCaption));
                }
                else
                {
                MessageBox.Show("Shared project has no active platform project");
                }
            }
            else
            {
                MessageBox.Show("Solution has no shared project");
                return;
            }
        }
        else
            {
                MessageBox.Show("No solution is open");
                return;
            }
        }
    }
    ```

12. 遍历平台项目。 以下方法获取共享项目中的所有导入（平台）项目。

    ```csharp
    private IEnumerable<IVsHierarchy> EnumImportingProjects(IVsHierarchy hierarchy)
    {
        IVsSharedAssetsProject sharedAssetsProject;
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,
            (int)__VSHPROPID7.VSHPROPID_SharedAssetsProject, out sharedAssetsProject)
            && sharedAssetsProject != null)
        {
            foreach (IVsHierarchy importingProject in sharedAssetsProject.EnumImportingProjects())
            {
                yield return importingProject;
            }
        }
    }
    ```

    > [!IMPORTANT]
    > 如果用户已在实验实例C++中打开通用 Windows 应用项目，上述代码将引发异常。 这是一个已知问题。 若要避免此异常，请将上述 `foreach` 块替换为以下内容：

    ```csharp
    var importingProjects = sharedAssetsProject.EnumImportingProjects();
    for (int i = 0; i < importingProjects.Count; ++i)
    {
        yield return importingProjects[i];
    }
    ```

13. 在 `ShowMessageBox` 方法中，输出每个平台项目的标题。 在输出活动平台项目标题的行的后面插入以下代码。 此列表中仅显示已加载的平台项目。

    ```csharp
    output.OutputStringThreadSafe("Platform projects:\n");

    IEnumerable<IVsHierarchy> projects = this.EnumImportingProjects(sharedHier);

    bool isActiveProjectSet = false;
    foreach (IVsHierarchy platformHier in projects)
    {
        string platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,
            (int)__VSHPROPID.VSHPROPID_Caption);
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));
    }
    ```

14. 更改 "活动平台" 项目。 下面的方法使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A> 设置活动项目。

    ```csharp
    private int SetActiveProjectContext(IVsHierarchy hierarchy, IVsHierarchy activeProjectContext)
    {
        return hierarchy.SetProperty((uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, activeProjectContext);
    }
    ```

15. 在 `ShowMessageBox` 方法中，更改 "活动平台" 项目。 将此代码插入 `foreach` 块中。

    ```csharp
    bool isActiveProjectSet = false;
    string platformCaption = null;
    foreach (IVsHierarchy platformHier in projects)
    {
        platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,
             (int)__VSHPROPID.VSHPROPID_Caption);
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));

        // if this project is neither the shared project nor the current active platform project,
        // set it to be the active project
        if (!isActiveProjectSet && platformHier != activePlatformHier)
        {
            this.SetActiveProjectContext(sharedHier, platformHier);
            activePlatformHier = platformHier;
            isActiveProjectSet = true;
        }
    }
    output.OutputStringThreadSafe("set active project: " + platformCaption +'\n');
    ```

16. 现在试试看。按 F5 启动实验实例。 在实验C#实例中创建通用中心应用项目（在 "**新建项目**" 对话框中， **Visual C#**   > **windows**  > **windows 8**  > **通用**0**中心应用**）。 加载解决方案后，请切换到 "**工具**" 菜单，单击 "**调用 TestUniversalProject**"，然后在 "**输出**" 窗格中查看文本。 显示的内容应与以下类似：

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    ```

### <a name="manage-the-shared-items-in-the-platform-project"></a>管理平台项目中的共享项

1. 在平台项目中查找共享项。 共享项目中的项在平台项目中显示为共享项。 你无法在**解决方案资源管理器**中查看它们，但你可以浏览项目层次结构来查找它们。 下面的方法遍历层次结构并收集所有共享项。 它还可以输出每个项的标题。 共享项由 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_IsSharedItem> 的新属性标识。

    ```csharp
    private void InspectHierarchyItems(IVsHierarchy hier, uint itemid, int level, List<uint> itemIds, bool getSharedItems, bool printItems)
    {
        string caption = HierarchyUtilities.GetHierarchyProperty<string>(hier, itemid, (int)__VSHPROPID.VSHPROPID_Caption);
        if (printItems)
            output.OutputStringThreadSafe(string.Format("{0}{1}\n", new string('\t', level), caption));

        // if getSharedItems is true, inspect only shared items; if it's false, inspect only unshared items
        bool isSharedItem;
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID7.VSHPROPID_IsSharedItem, out isSharedItem)
            && (isSharedItem == getSharedItems))
        {
            itemIds.Add(itemid);
        }

        uint child;
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID.VSHPROPID_FirstChild, Unbox.AsUInt32, out child)
            && child != (uint)VSConstants.VSITEMID.Nil)
        {
            this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);

            while (HierarchyUtilities.TryGetHierarchyProperty(hier, child, (int)__VSHPROPID.VSHPROPID_NextSibling, Unbox.AsUInt32, out child)
                && child != (uint)VSConstants.VSITEMID.Nil)
            {
                this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);
            }
                    }
    }
    ```

2. 在 `ShowMessageBox` 方法中，添加以下代码来演练平台项目层次结构项。 将其插入 `foreach` 块内。

    ```csharp
    output.OutputStringThreadSafe("Walk the active platform project:\n");
    var sharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ```

3. 读取共享项。 共享项作为隐藏链接文件显示在平台项目中，您可以将所有属性作为普通链接文件读取。 下面的代码读取第一个共享项的完整路径。

    ```csharp
    var sharedItemId = sharedItemIds[0];
    string fullPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared item full path: {0}\n", fullPath));
    ```

4. 现在试试看。按**F5**启动实验实例。 在实验C#实例中创建通用中心应用项目（在 "**新建项目**" 对话框中， **Visual C#**   > **windows**  > **windows 8**  > **通用**0**中心应用**）中转到 "**工具**" 菜单，单击 "**调用 TestUniversalProject**"，然后在 "**输出**" 窗格中检查文本。 显示的内容应与以下类似：

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    Walk the active platform project:
        HubApp.WindowsPhone
            <HubApp.Shared>
                App.xaml
                    App.xaml.cs
                Assets
                    DarkGray.png
                    LightGray.png
                    MediumGray.png
                Common
                    NavigationHelper.cs
                    ObservableDictionary.cs
                    RelayCommand.cs
                    SuspensionManager.cs
                DataModel
                    SampleData.json
                    SampleDataSource.cs
                HubApp.Shared.projitems
                Strings
                    en-US
                        Resources.resw
            Assets
                HubBackground.theme-dark.png
                HubBackground.theme-light.png
                Logo.scale-240.png
                SmallLogo.scale-240.png
                SplashScreen.scale-240.png
                Square71x71Logo.scale-240.png
                StoreLogo.scale-240.png
                WideLogo.scale-240.png
            HubPage.xaml
                HubPage.xaml.cs
            ItemPage.xaml
                ItemPage.xaml.cs
            Package.appxmanifest
            Properties
                AssemblyInfo.cs
            References
                .NET for Windows Store apps
                HubApp.Shared
                Windows Phone 8.1
            SectionPage.xaml
                SectionPage.xaml.cs
    ```

### <a name="detect-changes-in-platform-projects-and-shared-projects"></a>检测平台项目和共享项目中的更改

1. 您可以使用层次结构和项目事件来检测共享项目中的更改，就像对平台项目一样。 但是，共享项目中的项目项是不可见的，这意味着在更改共享项目项时，某些事件不会激发。

    重命名项目中的文件时，请考虑事件的顺序：

   1. 在磁盘上更改文件名。

   2. 项目文件将更新为包含文件的新名称。

      层次结构事件（例如 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>）通常跟踪 UI 中显示的更改，如**解决方案资源管理器**中所示。 层次结构事件将文件重命名操作视为包含文件删除和文件添加操作。 但是，当不可见项发生更改时，层次结构事件系统将引发 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 事件，但不会引发 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 事件。 因此，如果重命名平台项目中的文件，则会同时获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>，但是如果在共享项目中重命名文件，则仅会获得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>。

      若要跟踪项目项的更改，可以处理 DTE 项目项事件（在 <xref:EnvDTE.ProjectItemsEventsClass> 中找到的事件）。 但是，如果要处理大量事件，可以更好地处理 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 中的事件。 在本演练中，我们只显示层次结构事件和 DTE 事件。 在此过程中，您将向共享项目和平台项目中添加一个事件侦听器。 然后，当你重命名共享项目中的一个文件和平台项目中的另一个文件时，可以查看为每个重命名操作触发的事件。

      在此过程中，您将向共享项目和平台项目中添加一个事件侦听器。 然后，当你重命名共享项目中的一个文件和平台项目中的另一个文件时，可以查看为每个重命名操作触发的事件。

2. 添加事件侦听器。 向项目中添加一个新的类文件，并将其称为 " *HierarchyEventListener.cs*"。

3. 打开*HierarchyEventListener.cs*文件并添加以下 using 指令：

   ```csharp
   using Microsoft.VisualStudio.Shell.Interop;
   using Microsoft.VisualStudio;
   using System.IO;
   ```

4. 让 `HierarchyEventListener` 类实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>：

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   { }
   ```

5. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> 的成员，如下面的代码所示。

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   {
       private IVsHierarchy hierarchy;
       IVsOutputWindowPane output;

       internal HierarchyEventListener(IVsHierarchy hierarchy, IVsOutputWindowPane outputWindow) {
            this.hierarchy = hierarchy;
            this.output = outputWindow;
       }

       int IVsHierarchyEvents.OnInvalidateIcon(IntPtr hIcon) {
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnInvalidateItems(uint itemIDParent) {
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemAdded(uint itemIDParent, uint itemIDSiblingPrev, uint itemIDAdded) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemAdded: " + itemIDAdded + "\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemDeleted(uint itemID) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemDeleted: " + itemID + "\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemsAppended(uint itemIDParent) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemsAppended\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnPropertyChanged(uint itemID, int propID, uint flags) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnPropertyChanged: item ID " + itemID + "\n");
           return VSConstants.S_OK;
       }
   }
   ```

6. 在同一个类中，为 DTE 事件添加另一个事件处理程序 <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>，每当重命名项目项时都会发生这种情况。

   ```csharp
   public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)
   {
       output.OutputStringThreadSafe(string.Format("[Event] Renamed {0} to {1} in project {2}\n",
            oldName, Path.GetFileName(projItem.get_FileNames(1)), projItem.ContainingProject.Name));
   }
   ```

7. 注册层次结构事件。 需要为要跟踪的每个项目单独进行注册。 将以下代码添加到 `ShowMessageBox` 中，一个用于共享项目，另一个用于某个平台项目。

   ```csharp
   // hook up the event listener for hierarchy events on the shared project
   HierarchyEventListener listener1 = new HierarchyEventListener(sharedHier, output);
   uint cookie1;
   sharedHier.AdviseHierarchyEvents(listener1, out cookie1);

   // hook up the event listener for hierarchy events on the
   active project
   HierarchyEventListener listener2 = new HierarchyEventListener(activePlatformHier, output);
   uint cookie2;
   activePlatformHier.AdviseHierarchyEvents(listener2, out cookie2);
   ```

8. 注册 DTE 项目项事件 <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>。 在挂钩第二个侦听器后，添加以下代码。

   ```csharp
   // hook up DTE events for project items
   Events2 dteEvents = (Events2)dte.Events;
   dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;
   ```

9. 修改共享项。 不能修改平台项目中的共享项;相反，你必须在作为这些项的实际所有者的共享项目中对其进行修改。 你可以通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> 获取共享项目中的相应项 ID，并为其提供共享项的完整路径。 然后，可以修改共享项。 更改将传播到平台项目。

    > [!IMPORTANT]
    > 在修改项目项之前，应查明项目项是否为共享项。

     下面的方法修改项目项文件的名称。

    ```csharp
    private void ModifyFileNameInProject(IVsHierarchy project, string path)
    {
        int found;
        uint projectItemID;
        VSDOCUMENTPRIORITY[] priority = new VSDOCUMENTPRIORITY[1];
        if (ErrorHandler.Succeeded(((IVsProject)project).IsDocumentInProject(path, out found, priority, out projectItemID))
            && found != 0)
        {
            var name = DateTime.Now.Ticks.ToString() + Path.GetExtension(path);
            project.SetProperty(projectItemID, (int)__VSHPROPID.VSHPROPID_EditLabel, name);
            output.OutputStringThreadSafe(string.Format("Renamed {0} to {1}\n", path,name));
        }
    }
    ```

10. 在 `ShowMessageBox` 中的所有其他代码之后调用此方法，以修改共享项目中的项的文件名。 将此项插入到共享项目中获取项的完整路径的代码之后。

    ```csharp
    // change the file name of an item in a shared project
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared project item ID = {0}, full path = {1}\n", sharedItemId, fullPath));
    this.ModifyFileNameInProject(sharedHier, fullPath);
    ```

11. 生成并运行该项目。 在实验C#实例中创建通用集线器应用，请在 "**工具**" 菜单中单击 "**调用 TestUniversalProject**"，然后在 "常规输出" 窗格中检查文本。 共享项目中第一项的名称（我们希望它是*app.xaml*文件）应更改，你应看到 <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> 事件已激发。 在这种情况下，由于重命名*app.config*会导致*App.xaml.cs*被重命名，应会看到四个事件（每个平台项目两个）。 （DTE 事件不跟踪共享项目中的项。）应会看到两个 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 事件（每个平台项目一个事件），但没有 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 事件。

12. 现在，请尝试在平台项目中重命名文件，然后可以看到触发的事件之间的差异。 在调用 `ModifyFileName` 之后 `ShowMessageBox` 中添加以下代码。

    ```csharp
    // change the file name of an item in a platform project
    var unsharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, unsharedItemIds, false, false);

    var unsharedItemId = unsharedItemIds[0];
    string unsharedPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(unsharedItemId, out unsharedPath));
    output.OutputStringThreadSafe(string.Format("Platform project item ID = {0}, full path = {1}\n", unsharedItemId, unsharedPath));

    this.ModifyFileNameInProject(activePlatformHier, unsharedPath);
    ```

13. 生成并运行该项目。 在实验C#实例中创建通用项目，请在 "**工具**" 菜单中，单击 "**调用 TestUniversalProject**"，然后检查 "常规输出" 窗格中的文本。 重命名平台项目中的文件后，应会看到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 事件和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 事件。 因为更改文件会导致不更改其他文件，而且由于对平台项目中的项进行的更改不会传播到任何位置，因此，其中只有一个事件。
