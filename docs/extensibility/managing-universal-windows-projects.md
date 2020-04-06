---
title: 管理通用 Windows 项目 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 47926aa1-3b41-410d-bca8-f77fc950cbe7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fbbf9b6aaf983bb36291611a7b9b50f7886915b7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702688"
---
# <a name="manage-universal-windows-projects"></a>管理通用 Windows 项目

通用 Windows 应用是面向 Windows 8.1 和 Windows Phone 8.1 的应用，允许开发人员在这两个平台上使用代码和其他资产。 共享代码和资源保存在共享项目中，而特定于平台的代码和资源保存在单独的项目中，一个用于 Windows，另一个用于 Windows Phone。 有关通用 Windows 应用的详细信息，请参阅[通用 Windows 应用](https://msdn.microsoft.com/library/windows/apps/dn609832.aspx)。 管理项目的 Visual Studio 扩展应注意，通用 Windows 应用项目的结构不同于单平台应用。 本演练将介绍如何导航共享项目和管理共享项目。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="navigate-the-shared-project"></a>导航共享项目

1. 创建名为**TestUniversal 项目的**C# VSIX 项目。 （**文件** > **新项目** > **Project**，然后**C#** > **扩展可视化** > **工作室包**）。 添加**自定义命令**项目项模板（在**解决方案资源管理器**上，右键单击项目节点并选择 **"添加新** > **项**"，然后转到 **"扩展性**"。。 命名文件**TestUniversalProject**。

2. 添加对*Microsoft.VisualStudio.shell.Interop.12.1.DesignTime.dll*和*Microsoft.VisualStudio.shell.Interop.14.0.DesignTime.dll*的引用（在**扩展部分**）。

3. 打开*TestUniversalProject.cs*并添加以下`using`指令：

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

4. 在类`TestUniversalProject`中添加指向 **"输出"** 窗口的专用字段。

    ```csharp
    public sealed class TestUniversalProject
    {
        IVsOutputWindowPane output;
    . . .
    }
    ```

5. 在 TestUniversalProject 构造函数中设置对输出窗格的引用：

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

6. 从`ShowMessageBox`方法中删除现有代码：

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
    }
    ```

7. 获取 DTE 对象，在本演练中，我们将用于几个不同的用途。 此外，请确保在单击菜单按钮时加载解决方案。

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

8. 查找共享项目。 共享项目是一个纯容器;它不生成或生成输出。 以下方法通过查找具有共享项目功能<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>的对象来查找解决方案中的第一个共享项目。

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

9. 在`ShowMessageBox`方法中，输出共享项目的标题（出现在**解决方案资源管理器**中的项目名称）。

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

10. 获取活动平台项目。 平台项目是包含特定于平台的代码和资源的项目。 以下方法使用新字段<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy>获取活动平台项目。

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

11. 在`ShowMessageBox`该方法中，输出活动平台项目的标题。

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

12. 迭代平台项目。 以下方法从共享项目获取所有导入（平台）项目。

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
    > 如果用户已在实验实例中打开了C++通用 Windows 应用项目，则上述代码将引发异常。 这是一个已知问题。 为避免出现异常，请将上面`foreach`的块替换为以下内容：

    ```csharp
    var importingProjects = sharedAssetsProject.EnumImportingProjects();
    for (int i = 0; i < importingProjects.Count; ++i)
    {
        yield return importingProjects[i];
    }
    ```

13. 在`ShowMessageBox`该方法中，输出每个平台项目的标题。 在输出活动平台项目标题的行后插入以下代码。 只有加载的平台项目才会显示在此列表中。

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

14. 更改活动平台项目。 以下方法使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A>设置活动项目。

    ```csharp
    private int SetActiveProjectContext(IVsHierarchy hierarchy, IVsHierarchy activeProjectContext)
    {
        return hierarchy.SetProperty((uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, activeProjectContext);
    }
    ```

15. 在`ShowMessageBox`方法中，更改活动平台项目。 在`foreach`块内插入此代码。

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

16. 现在试试看。按 F5 启动实验实例。 在实验实例中创建 C# 通用中心应用项目（在 **"新项目**"对话框中 **，Visual C++** > **Windows** > **8** > **通用** > **中心应用**）。 加载解决方案后，转到 **"工具"** 菜单并单击 **"调用测试通用项目**"，然后检查 **"输出"** 窗格中的文本。 会看到下面这样的内容：

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    ```

### <a name="manage-the-shared-items-in-the-platform-project"></a>管理平台项目中的共享项目

1. 查找平台项目中的共享项目。 共享项目中的项目在平台项目中显示为共享项目。 在**解决方案资源管理器**中看不到它们，但可以遍历项目层次结构来查找它们。 以下方法遍走层次结构并收集所有共享项。 它可以选择输出每个项目的标题。 共享项由新属性<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_IsSharedItem>标识。

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

2. 在`ShowMessageBox`方法中，添加以下代码以遍历平台项目层次结构项。 将其插入块内`foreach`。

    ```csharp
    output.OutputStringThreadSafe("Walk the active platform project:\n");
    var sharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ```

3. 阅读共享项目。 共享项目在平台项目中显示为隐藏链接文件，您可以将所有属性读为普通链接文件。 以下代码读取第一个共享项的完整路径。

    ```csharp
    var sharedItemId = sharedItemIds[0];
    string fullPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared item full path: {0}\n", fullPath));
    ```

4. 现在试试看。按**F5**启动实验实例。 在实验实例中创建 C# 通用中心应用项目（在 **"新项目**"对话框中 **，Visual C++** > **Windows** > **8** > **通用** > **中心应用**）转到 **"工具"** 菜单并单击 **"调用测试通用项目**"，然后选中 **"输出**"窗格中的文本。 会看到下面这样的内容：

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

1. 您可以使用层次结构和项目事件来检测共享项目中的更改，就像对平台项目一样。 但是，共享项目中的项目项不可见，这意味着当更改共享项目项时，某些事件不会触发。

    在重命名项目中的文件时，请考虑事件序列：

   1. 文件名在磁盘上更改。

   2. 项目文件将更新以包括该文件的新名称。

      层次结构事件（例如<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>），通常跟踪 UI 中显示的更改，如**解决方案资源管理器**中所示。 层次结构事件考虑文件重命名操作，以包括文件删除，然后添加文件。 但是，当更改不可见项时，层次结构事件系统将触发事件<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>，但不会触发<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>事件。 因此，如果在平台项目中重命名文件，则获取 和<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>，但如果重命名共享项目中的文件，则仅<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>获取 。

      要跟踪项目项中的更改，可以处理 DTE 项目项事件（中找到的<xref:EnvDTE.ProjectItemsEventsClass>项事件）。 但是，如果您正在处理大量事件，则可以在 中<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>处理事件时获得更好的性能。 在本演练中，我们仅显示层次结构事件和 DTE 事件。 在此过程中，您将事件侦听器添加到共享项目和平台项目。 然后，当您重命名共享项目中的一个文件和平台项目中的另一个文件时，您可以看到为每个重命名操作触发的事件。

      在此过程中，您将事件侦听器添加到共享项目和平台项目。 然后，当您重命名共享项目中的一个文件和平台项目中的另一个文件时，您可以看到为每个重命名操作触发的事件。

2. 添加事件侦听器。 向项目添加新类文件，并将其调用*HierarchyEventListener.cs*。

3. 打开*HierarchyEventListener.cs*文件并添加以下使用指令：

   ```csharp
   using Microsoft.VisualStudio.Shell.Interop;
   using Microsoft.VisualStudio;
   using System.IO;
   ```

4. 具有类`HierarchyEventListener`实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>：

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   { }
   ```

5. 实现 的成员<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>，如下代码所示。

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

6. 在同一类中为 DTE 事件<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>添加另一个事件处理程序 ，每当重命名项目项时都会发生这种情况。

   ```csharp
   public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)
   {
       output.OutputStringThreadSafe(string.Format("[Event] Renamed {0} to {1} in project {2}\n",
            oldName, Path.GetFileName(projItem.get_FileNames(1)), projItem.ContainingProject.Name));
   }
   ```

7. 注册层次结构事件。 您需要为正在跟踪的每个项目分别注册。 在 中`ShowMessageBox`添加以下代码 ，一个用于共享项目，另一个用于其中一个平台项目。

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

8. 注册 DTE 项目项事件<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>。 挂接第二个侦听器后，添加以下代码。

   ```csharp
   // hook up DTE events for project items
   Events2 dteEvents = (Events2)dte.Events;
   dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;
   ```

9. 修改共享项。 不能修改平台项目中的共享项目;但是，您可以修改平台项目中的共享项目。相反，您必须在共享项目中修改它们，这些共享项目是这些项目的实际所有者。 您可以在 共享<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A>项目中获取相应的项目 ID，从而提供共享项的完整路径。 然后，您可以修改共享项。 更改将传播到平台项目。

    > [!IMPORTANT]
    > 在修改项目项之前，应先了解项目项是否为共享项。

     以下方法修改项目项文件的名称。

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

10. 在 中的所有其他代码之后`ShowMessageBox`调用此方法，以修改共享项目中的项目的文件名。 在获取共享项目中项目的完整路径的代码后插入此项。

    ```csharp
    // change the file name of an item in a shared project
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared project item ID = {0}, full path = {1}\n", sharedItemId, fullPath));
    this.ModifyFileNameInProject(sharedHier, fullPath);
    ```

11. 生成并运行该项目。 在实验实例中创建 C# 通用集线器应用，转到 **"工具"** 菜单并单击 **"调用测试通用项目**"，然后检查常规输出窗格中的文本。 应更改共享项目中第一个项目的名称（我们预计它是*App.xaml*文件），您应该看到<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>事件已触发。 在这种情况下，由于重命名*App.xaml*也会导致*App.xaml.cs*重命名，因此应看到四个事件（每个平台项目有两个事件）。 （DTE 事件不跟踪共享项目中的项目。您应该看到两<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>个事件（每个平台项目一个），但没有<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>事件。

12. 现在尝试重命名平台项目中的文件，您可以看到触发事件的差异。 在调用`ShowMessageBox`后将`ModifyFileName`以下代码添加到 。

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

13. 生成并运行该项目。 在实验实例中创建 C# 通用项目，转到 **"工具"** 菜单并单击 **"调用测试通用项目**"，然后检查常规输出窗格中的文本。 重命名平台项目中的文件后，应同时看到<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>事件和<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>事件。 由于更改文件不会更改其他文件，并且对平台项目中项的更改不会在任何地方传播，因此每个事件只有一个。
