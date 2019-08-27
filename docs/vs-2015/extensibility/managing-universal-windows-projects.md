---
title: 管理通用 Windows 项目 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 47926aa1-3b41-410d-bca8-f77fc950cbe7
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 08d88ce08c6c91cbf46bcc6d15cbf098d61e604d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65679930"
---
# <a name="managing-universal-windows-projects"></a>管理通用 Windows 项目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通用 Windows 应用是面向 Windows 8.1 和 Windows Phone 8.1，从而允许开发人员在这两个平台上使用的代码和其他资产。 共享的代码和资源都保存在共享项目，而特定于平台的代码和资源保留在单独的项目，一个用于 Windows，另一个用于 Windows Phone。 有关通用 Windows 应用程序的详细信息，请参阅[通用 Windows 应用](https://msdn.microsoft.com/library/windows/apps/dn609832.aspx)。 管理项目的 visual Studio 扩展应了解通用 Windows 应用项目具有不同于单平台的应用程序的结构。 本演练演示如何导航共享的项目和管理共享的项。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
### <a name="navigate-the-shared-project"></a>导航共享的项目  
  
1. 创建一个名为 C# VSIX 项目**TestUniversalProject**。 (**文件，新建、 项目**，然后**C#，可扩展性，Visual Studio 包**)。 添加**自定义命令**项目项模板 (在解决方案资源管理器，右键单击项目节点并选择**添加 / 新建项**，然后转到**扩展性**)。 将文件命名**TestUniversalProject**。  
  
2. 添加对 Microsoft.VisualStudio.Shell.Interop.12.1.DesignTime.dll 和 Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll 的引用 (在**扩展**部分)。  
  
3. 打开 TestUniversalProject.cs 并添加以下`using`语句：  
  
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
  
4. TestUniversalProject 类中添加一个指向的私有字段**输出**窗口。  
  
    ```csharp  
    public sealed class TestUniversalProject   
    {  
        IVsOutputWindowPane output;  
    . . .  
    }  
    ```  
  
5. 设置对 TestUniversalProject 构造函数内的输出窗格的引用：  
  
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
  
6. 删除从现有代码`ShowMessageBox`方法：  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)   
    {  
    }  
    ```  
  
7. 获取 DTE 对象，我们将使用在本演练中有多种不同的用途。 此外，请确保单击的菜单按钮时加载解决方案。  
  
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
  
8. 查找共享的项目。 共享的项目是一个纯粹的容器;它不生成或生成的输出。 以下方法通过查找在解决方案中查找第一个共享的项目<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>具有共享的项目功能的对象。  
  
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
  
9. 在中`ShowMessageBox`方法中，输出标题 (中显示的项目名称**解决方案资源管理器**) 的共享项目。  
  
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
  
10. 获取活动平台项目。 平台项目都包含特定于平台的代码和资源的项目。 以下方法使用新字段<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7>若要获取活动平台项目。  
  
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
  
11. 在`ShowMessageBox`方法中，输出活动平台项目的标题。  
  
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
  
    ```  
  
12. 循环访问平台项目。 以下方法获取从共享的项目导入的所有 （平台） 项目。  
  
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
    > 如果用户打开C++通用 Windows 应用项目中的实验实例中，上面的代码将引发异常。 这是一个已知问题。 若要避免此异常，将为`foreach`上面阻止以下：  
  
    ```csharp  
    var importingProjects = sharedAssetsProject.EnumImportingProjects();  
    for (int i = 0; i < importingProjects.Count; ++i)  
    {  
        yield return importingProjects[i];  
    }   
    ```  
  
13. 在`ShowMessageBox`方法中，输出每个平台项目的标题。 输出活动平台项目的标题的行后面插入以下代码。 此列表中显示已加载的平台项目。  
  
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
  
14. 更改活动平台项目。 以下方法设置活动项目使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A>。  
  
    ```csharp  
    private int SetActiveProjectContext(IVsHierarchy hierarchy, IVsHierarchy activeProjectContext)  
    {  
        return hierarchy.SetProperty((uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, activeProjectContext);  
    }  
    ```  
  
15. 在`ShowMessageBox`方法中，更改活动平台项目。 插入此代码`foreach`块。  
  
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
  
16. 现在试一试。按 F5 启动实验实例。 在实验实例中创建一个 C# 通用中心应用程序项目 (在**新的项目**对话框中， **Visual C# / Windows / Windows 8 / 通用 / 中心应用**)。 加载解决方案后，请转到**工具**菜单，然后单击**调用 TestUniversalProject**，然后再签入文本**输出**窗格。 显示的内容应与以下类似：  
  
    ```  
    Found shared project: HubApp.Shared  
    The active platform project: HubApp.Windows  
    Platform projects:  
     * HubApp.Windows  
     * HubApp.WindowsPhone  
    set active project: HubApp.WindowsPhone  
    ```  
  
### <a name="manage-the-shared-items-in-the-platform-project"></a>管理平台项目中的共享的项  
  
1. 查找在平台项目中共享的项。 共享项目中的项在平台项目中显示为共享项。 你不能看到它们在**解决方案资源管理器**，但您可以放心离开项目层次结构，可以找到它们。 以下方法将在层次结构的指导，并收集所有共享的项。 它根据需要将输出的每个项的标题。 通过新的属性标识的共享的项<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7>。  
  
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
  
2. 在`ShowMessageBox`方法中，添加以下代码以引导平台项目层次结构项。 插入内`foreach`块。  
  
    ```csharp  
    output.OutputStringThreadSafe("Walk the active platform project:\n");  
    var sharedItemIds = new List<uint>();  
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);  
    ```  
  
3. 读取共享的项目。 共享的项在平台项目中显示为隐藏的链接文件，并可以读取为普通链接的文件的所有属性。 以下代码将读取第一个共享项的完整路径。  
  
    ```csharp  
    var sharedItemId = sharedItemIds[0];  
    string fullPath;  
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));  
    output.OutputStringThreadSafe(string.Format("Shared item full path: {0}\n", fullPath));  
    ```  
  
4. 现在试一试。按 F5 启动实验实例。 在实验实例中创建一个 C# 通用中心应用程序项目 (在**新的项目**对话框中， **Visual C# / Windows / Windows 8 / 通用 / 中心应用**) 转到**工具**菜单，然后单击**调用 TestUniversalProject**，然后再签入文本**输出**窗格。 显示的内容应与以下类似：  
  
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
  
### <a name="detecting-changes-in-platform-projects-and-shared-projects"></a>检测平台项目和共享的项目中的更改  
  
1. 正如平台项目，您可以使用层次结构和项目事件在共享项目中，检测更改。 但是，共享项目中的项目项不可见，这意味着更改共享的项目项时，某些事件不会发生激发。  
  
    请考虑重命名项目中的文件时的事件序列：  
  
   1. 在磁盘上更改的文件的名称。  
  
   2. 更新项目文件以包括新的文件的名称。  
  
      层次结构事件 (例如， <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>) 通常可跟踪所做的更改显示在 UI 中，如**解决方案资源管理器**。 层次结构事件，请考虑删除文件和文件添加然后组成的文件重命名操作。 但是，不可见的项更改时，层次结构事件系统会触发<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>事件，但不是<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>事件。 因此，如果您重命名的平台项目中的文件，则获取这两项<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>并<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>，但如果您重命名共享项目中的文件，则仅获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>。  
  
      若要跟踪项目项中的更改，你可以处理 DTE 项目项事件 (在中找到的<xref:EnvDTE.ProjectItemsEventsClass>)。 但是，如果要处理大量的事件，你可以获得更好的性能处理中的事件<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>。 在本演练中介绍的层次结构事件以及 DTE 事件。 在此过程中对共享的项目和平台项目添加事件侦听器。 然后，当您重命名共享项目中的一个文件，并在平台项目中的另一个文件，可以看到为每个重命名操作激发的事件。  
  
      在此过程中对共享的项目和平台项目添加事件侦听器。 然后，当您重命名共享项目中的一个文件，并在平台项目中的另一个文件，可以看到为每个重命名操作激发的事件。  
  
2. 添加事件侦听器。 向项目添加一个新类文件，并调用它 HierarchyEventListener.cs。  
  
3. 打开 HierarchyEventListener.cs 文件并添加以下 using 语句：  
  
   ```csharp  
   using Microsoft.VisualStudio.Shell.Interop;  
   using Microsoft.VisualStudio;  
   using System.IO;  
  
   ```  
  
4. 具有`HierarchyEventListener`类实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>:  
  
   ```csharp  
   class HierarchyEventListener : IVsHierarchyEvents  
   { }  
  
   ```  
  
5. 实现的成员<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>，如下面的代码。  
  
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
  
6. 在同一类中添加另一个事件处理程序 DTE 事件<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>，就会出现此每当重命名项目项。  
  
   ```csharp  
   public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)  
   {  
       output.OutputStringThreadSafe(string.Format("[Event] Renamed {0} to {1} in project {2}\n",  
            oldName, Path.GetFileName(projItem.get_FileNames(1)), projItem.ContainingProject.Name));  
   }  
   ```  
  
7. 注册层次结构事件。 您需要单独登录正在跟踪每个项目。 中的以下代码添加`ShowMessageBox`，一个用于共享的项目，另一个用于平台项目之一。  
  
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
  
8. DTE 项目项事件注册<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>。 可以将挂接到第二个侦听器后，请添加以下代码。  
  
   ```csharp  
   // hook up DTE events for project items  
   Events2 dteEvents = (Events2)dte.Events;  
   dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;  
  
   ```  
  
9. 修改共享的项。 不能修改平台项目; 中的共享的项相反，必须在这些项的实际所有者共享项目中修改它们。 可以使用共享项目中获取相应的项 ID <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A>，向其提供共享的项的完整路径。 然后，可以修改共享的项。 更改传播到平台项目。  
  
    > [!IMPORTANT]
    > 您应找出项目项是共享的项之前修改它。  
  
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
  
10. 调用此方法，别忘了中的其他代码`ShowMessageBox`若要修改的文件的名称在共享项目中的项。 共享项目中获取的项的完整路径的代码后面插入此操作。  
  
    ```csharp  
    // change the file name of an item in a shared project  
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);  
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));   
    output.OutputStringThreadSafe(string.Format("Shared project item ID = {0}, full path = {1}\n", sharedItemId, fullPath));  
    this.ModifyFileNameInProject(sharedHier, fullPath);  
    ```  
  
11. 生成并运行该项目。 在实验实例中创建一个 C# 通用中心应用程序，请转到**工具**菜单，然后单击**调用 TestUniversalProject**，并检查常规输出窗格中的文本。 在共享的第一项的名称 （我们希望它是 App.xaml 文件） 的项目应进行更改，因此您应该会看到<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>触发事件。 在这种情况下，重命名 App.xaml 导致 App.xaml.cs 也要重命名，因为您应看到四个事件 （对于每个平台项目的两个）。 （DTE 事件不跟踪共享项目中的项。）您应看到两个<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>事件 （一个是为每个平台项目中），但不是<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>事件。  
  
12. 现在，尝试重命名在平台项目中，文件，可以看到中获取触发的事件的差异。 将以下代码中的添加`ShowMessageBox`调用的后面`ModifyFileName`。  
  
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
  
13. 生成并运行该项目。 在实验实例中创建一个 C# 通用项目，请转到**工具**菜单，然后单击**调用 TestUniversalProject**，并检查常规输出窗格中的文本。 平台项目中的文件重命名后，你应看到<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>事件和一个<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>事件。 更改以来该文件将导致其他文件来更改，并且由于平台项目中的项的更改不获取任何位置传播，因此没有仅每个上述事件之一。
