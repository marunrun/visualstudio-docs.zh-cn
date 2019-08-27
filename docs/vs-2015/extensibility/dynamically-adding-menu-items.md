---
title: 动态添加菜单项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- DYNAMICITEMSTART
- menu items, adding dynamically
- menus, adding dynamic items
ms.assetid: d281e9c9-b289-4d64-8d0a-094bac6c333c
caps.latest.revision: 38
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 45d435a9c77d63fbd1e92a7615df232c2a0cc117
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62555512"
---
# <a name="dynamically-adding-menu-items"></a>动态添加菜单项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以通过指定在运行时添加菜单项`DynamicItemStart`命令标志中的占位符按钮定义在 Visual Studio 命令表格 (.vsct) 文件，然后定义 （在代码中） 数的菜单项来显示和处理命令。 加载 VSPackage 时，包含动态菜单项会替换占位符。  
  
 Visual Studio 将使用中的动态列表**最近使用过**(MRU) 列表中，后者将显示最近打开的文档的名称，并**Windows**列表，显示的 windows 名称当前打开的。   `DynamicItemStart`标志上的命令定义指定的命令是一个占位符，直到打开 VSPackage。 当打开 VSPackage 时，占位符将被替换 0 或更多命令在运行时创建并添加到动态列表。 您不能以查看其中动态列表之前打开 VSPackage 时，会显示在菜单上的位置。  若要填充的动态列表，Visual Studio 会询问要查找其第一个字符是占位符的 ID 相同的 ID 与命令的 VSPackage。 当 Visual Studio 找到匹配的命令时，它将命令的名称添加到动态列表。 然后它递增 ID，并查找另一个匹配的命令，直到没有更多动态命令将添加到动态列表。  
  
 本演练演示如何设置启动项目在 Visual Studio 解决方案中使用命令**解决方案资源管理器**工具栏。 它使用活动解决方案中有一个项目的动态下拉列表菜单控制器。 若要防止此命令显示时没有解决方案处于打开状态或仅当解决方案包含多个项目时打开的解决方案具有只有一个项目，加载 VSPackage。  
  
 有关.vsct 文件的详细信息，请参阅[Visual Studio 命令表 (。Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。  
  
## <a name="creating-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展  
  
1. 创建一个名为的 VSIX 项目`DynamicMenuItems`。  
  
2. 当项目打开时，添加自定义命令项模板并将其命名**DynamicMenu**。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
## <a name="setting-up-the-elements-in-the-vsct-file"></a>.Vsct 文件中的元素的设置  
 若要创建工具栏上的动态菜单项的菜单控制器，你可以指定以下元素：  
  
- 两个命令组、 一个包含菜单控制器和另一个同时包含下拉列表中的菜单项  
  
- 类型的一个菜单元素 `MenuController`  
  
- 两个按钮，一个充当提供图标，并在工具栏上的工具提示的菜单项，另一个占位符。  
  
1. DynamicMenuPackage.vsct 中, 定义的命令 Id。 转到符号部分并替换在 IDSymbol 元素**guidDynamicMenuPackageCmdSet** GuidSymbol 块。 您需要定义 IDSymbol 元素的两个组、 菜单控制器、 占位符命令和定位点命令。  
  
    ```csharp  
    <GuidSymbol name="guidDynamicMenuPackageCmdSet" value="{ your GUID here }">  
        <IDSymbol name="MyToolbarItemGroup" value="0x1020" />  
        <IDSymbol name="MyMenuControllerGroup" value="0x1025" />  
        <IDSymbol name="MyMenuController" value ="0x1030"/>  
        <IDSymbol name="cmdidMyAnchorCommand" value="0x0103" />  
        <!-- NOTE: The following command expands at run time to some number of ids.  
         Try not to place command ids after it (e.g. 0x0105, 0x0106).  
         If you must add a command id after it, make the gap very large (e.g. 0x200) -->  
        <IDSymbol name="cmdidMyDynamicStartCommand" value="0x0104" />  
    </GuidSymbol>    
    ```  
  
2. 在组部分中，删除现有组并添加您刚定义的两个组：  
  
    ```  
    <Groups>  
        <!-- The group that adds the MenuController on the Solution Explorer toolbar.   
             The 0x4000 priority adds this group after the group that contains the  
             Preview Selected Items button, which is normally at the far right of the toolbar. -->  
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" priority="0x4000" >  
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN" />  
        </Group>  
        <!-- The group for the items on the MenuController drop-down. It is added to the MenuController submenu. -->  
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" priority="0x4000" >  
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" />  
        </Group>  
    </Groups>  
    ```  
  
     添加 MenuController。 设置 DynamicVisibility 命令标志，因为它不是始终可见。 不显示 ButtonText。  
  
    ```  
    <Menus>  
        <!-- The MenuController to display on the Solution Explorer toolbar.  
             Place it in the ToolbarItemGroup.-->  
        <Menu guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" priority="0x1000" type="MenuController">  
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" />  
            <CommandFlag>DynamicVisibility</CommandFlag>  
            <Strings>  
               <ButtonText></ButtonText>  
           </Strings>  
        </Menu>  
    </Menus>  
    ```  
  
3. 为 MenuController 添加两个按钮，一个作为动态菜单项的占位符，一个为定位点。  
  
     占位符按钮的父级是**MyMenuControllerGroup**。 将 DynamicItemStart、 DynamicVisibility 和 TextChanges 命令标志添加到占位符按钮。 不显示 ButtonText。  
  
     定位点按钮保存图标和工具提示文本。 定位点按钮的父级是还**MyMenuControllerGroup**。 添加 NoShowOnMenuController 命令标志来确保按钮实际上不会出现在菜单的控制器下拉列表中和 FixMenuController 命令标志，以使其永久定位点。  
  
    ```  
    <!-- The placeholder for the dynamic items that expand to N items at runtime. -->  
    <Buttons>  
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyDynamicStartCommand" priority="0x1000" >  
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />  
          <CommandFlag>DynamicItemStart</CommandFlag>  
          <CommandFlag>DynamicVisibility</CommandFlag>  
          <CommandFlag>TextChanges</CommandFlag>  
          <!-- This text does not appear. -->  
          <Strings>  
            <ButtonText>Project</ButtonText>  
          </Strings>  
        </Button>  
  
        <!-- The anchor item to supply the icon/tooltip for the MenuController -->  
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyAnchorCommand" priority="0x0000" >  
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />  
          <!-- This is the icon that appears on the Solution Explorer toolbar. -->  
          <Icon guid="guidImages" id="bmpPicArrows"/>  
          <!-- Do not show on the menu controller's drop down list-->  
          <CommandFlag>NoShowOnMenuController</CommandFlag>  
          <!-- Become the permanent anchor item for the menu controller -->  
          <CommandFlag>FixMenuController</CommandFlag>  
          <!-- The text that appears in the tooltip.-->  
          <Strings>  
            <ButtonText>Set Startup Project</ButtonText>  
          </Strings>  
        </Button>  
    </Buttons>  
    ```  
  
4. 将图标添加到项目 （在资源文件夹中），并在.vsct 文件中添加对它的引用。 在本演练中，我们将使用项目模板中包含的箭头图标。  
  
5. 添加 VisibilityConstraints 部分外部之前的 Symbols 部分的命令部分。 （如果将其添加符号后可能会收到一条警告。）本部分可确保菜单控制器仅在加载具有多个项目的解决方案时将出现。  
  
    ```  
    <VisibilityConstraints>  
         <!--Make the MenuController show up only when there is a solution with more than one project loaded-->  
        <VisibilityItem guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" context="UICONTEXT_SolutionHasMultipleProjects"/>  
    </VisibilityConstraints>  
    ```  
  
## <a name="implementing-the-dynamic-menu-command"></a>实现动态菜单命令  
 创建动态菜单命令类，该类继承<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>。 在此实现中，构造函数指定一个谓词，用于匹配的命令。 必须重写<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A>方法，若要使用此谓词设置<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A>属性，用于标识要调用的命令。  
  
1. 创建一个新 C# 类文件命名为 DynamicItemMenuCommand.cs，并添加名为的类**DynamicItemMenuCommand** ，它继承自<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>:  
  
    ```csharp  
    class DynamicItemMenuCommand : OleMenuCommand  
    {  
  
    }  
  
    ```  
  
2. 添加以下 using 语句：  
  
    ```csharp  
    using Microsoft.VisualStudio.Shell;  
    using Microsoft.VisualStudio.Shell.Interop;  
    using System.ComponentModel.Design;  
    ```  
  
3. 添加一个私有字段以存储匹配谓词：  
  
    ```csharp  
    private Predicate<int> matches;  
  
    ```  
  
4. 添加继承的构造函数<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>构造函数，并指定命令处理程序和一个<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>处理程序。 添加一个谓词匹配的命令：  
  
    ```csharp  
    public DynamicItemMenuCommand(CommandID rootId, Predicate<int> matches, EventHandler invokeHandler, EventHandler beforeQueryStatusHandler)  
        : base(invokeHandler, null /*changeHandler*/, beforeQueryStatusHandler, rootId)  
    {  
        if (matches == null)  
        {  
            throw new ArgumentNullException("matches");  
        }  
  
        this.matches = matches;  
    }  
    ```  
  
5. 重写<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A>方法以便调用匹配谓词和集<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A>属性：  
  
    ```csharp  
    public override bool DynamicItemMatch(int cmdId)  
    {  
        // Call the supplied predicate to test whether the given cmdId is a match.  
        // If it is, store the command id in MatchedCommandid   
        // for use by any BeforeQueryStatus handlers, and then return that it is a match.  
        // Otherwise clear any previously stored matched cmdId and return that it is not a match.  
        if (this.matches(cmdId))  
        {  
            this.MatchedCommandId = cmdId;  
            return true;  
        }  
  
        this.MatchedCommandId = 0;  
        return false;  
    }  
    ```  
  
## <a name="adding-the-command"></a>添加命令  
 DynamicMenu 构造函数是在其中设置菜单命令，其中包括动态菜单和菜单项。  
  
1. 在 DynamicMenuPackageGuids.cs，添加的命令集的 GUID 和命令 ID:  
  
    ```csharp  
    public const string guidDynamicMenuPackageCmdSet = "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file  
    public const uint cmdidMyCommand = 0x104;  
    ```  
  
2. 在 DynamicMenu.cs 文件中，添加以下 using 语句：  
  
    ```csharp  
    using EnvDTE;  
    using EnvDTE80;  
    using System.ComponentModel.Design;  
    ```  
  
3. 在 DynamicMenu 类中，添加一个私有字段**dte2**。  
  
    ```csharp  
    private DTE2 dte2;  
    ```  
  
4. 添加专用 rootItemId 字段：  
  
    ```csharp  
    private int rootItemId = 0;  
    ```  
  
5. 在 DynamicMenu 构造函数中，添加菜单命令。 下一节中，我们将定义命令处理程序，`BeforeQueryStatus`事件处理程序，并匹配谓词。  
  
    ```csharp  
    private DynamicMenu(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            // Add the DynamicItemMenuCommand for the expansion of the root item into N items at run time.   
            CommandID dynamicItemRootId = new CommandID(new Guid(DynamicMenuPackageGuids.guidDynamicMenuPackageCmdSet), (int)DynamicMenuPackageGuids.cmdidMyCommand);  
            DynamicItemMenuCommand dynamicMenuCommand = new DynamicItemMenuCommand(dynamicItemRootId,  
                IsValidDynamicItem,  
                OnInvokedDynamicItem,  
                OnBeforeQueryStatusDynamicItem);  
                commandService.AddCommand(dynamicMenuCommand);  
                }  
  
        dte2 = (DTE2)this.ServiceProvider.GetService(typeof(DTE));  
    }  
    ```  
  
## <a name="implementing-the-handlers"></a>实现处理程序  
 若要在菜单控制器上实现动态菜单项，必须单击动态项时处理该命令。 此外必须实现设置菜单项的状态的逻辑。 将处理程序添加到 DynamicMenu 类。  
  
1. 若要实现**设置启动项目**命令，添加**OnInvokedDynamicItem**事件处理程序。 它会查找其名称是相同的调用，并将其设置为启动项目中设置其绝对路径的命令文本的项目<xref:EnvDTE.SolutionBuild.StartupProjects%2A>属性。  
  
    ```csharp  
    private void OnInvokedDynamicItem(object sender, EventArgs args)  
    {  
        DynamicItemMenuCommand invokedCommand = (DynamicItemMenuCommand)sender;  
        // If the command is already checked, we don’t need to do anything  
        if (invokedCommand.Checked)  
            return;  
  
        // Find the project that corresponds to the command text and set it as the startup project  
        var projects = dte2.Solution.Projects;  
        foreach (Project proj in projects)  
        {  
            if (invokedCommand.Text.Equals(proj.Name))  
            {  
                dte2.Solution.SolutionBuild.StartupProjects = proj.FullName;  
                return;  
            }  
        }  
    }  
    ```  
  
2. 添加`OnBeforeQueryStatusDynamicItem`事件处理程序。 这是处理程序之前调用`QueryStatus`事件。 它确定菜单项是否是"真正的"项，也就是说，不的占位符项，以及是否已选中项 （即该项目已设置为启动项目）。  
  
    ```csharp  
    private void OnBeforeQueryStatusDynamicItem(object sender, EventArgs args)  
    {  
        DynamicItemMenuCommand matchedCommand = (DynamicItemMenuCommand)sender;  
        matchedCommand.Enabled = true;  
        matchedCommand.Visible = true;  
  
        // Find out whether the command ID is 0, which is the ID of the root item.  
        // If it is the root item, it matches the constructed DynamicItemMenuCommand,  
         // and IsValidDynamicItem won't be called.  
        bool isRootItem = (matchedCommand.MatchedCommandId == 0);  
  
        // The index is set to 1 rather than 0 because the Solution.Projects collection is 1-based.  
        int indexForDisplay = (isRootItem ? 1 : (matchedCommand.MatchedCommandId - (int) DynamicMenuPackageGuids.cmdidMyCommand) + 1);  
  
        matchedCommand.Text = dte2.Solution.Projects.Item(indexForDisplay).Name;  
  
        Array startupProjects = (Array)dte2.Solution.SolutionBuild.StartupProjects;  
        string startupProject = System.IO.Path.GetFileNameWithoutExtension((string)startupProjects.GetValue(0));  
  
        // Check the command if it isn't checked already selected  
        matchedCommand.Checked = (matchedCommand.Text == startupProject);  
  
        // Clear the ID because we are done with this item.  
        matchedCommand.MatchedCommandId = 0;  
    }  
    ```  
  
## <a name="implementing-the-command-id-match-predicate"></a>实现命令 ID 匹配谓词  
  
1. 现在，实现匹配谓词。 我们需要确定两件事： 首先，命令 ID 是否有效 （它是大于或等于声明的命令 ID），和第二个，它是否指定可能的项目 （它是解决方案中的项目数小于）。  
  
    ```csharp  
    private bool IsValidDynamicItem(int commandId)  
    {  
        // The match is valid if the command ID is >= the id of our root dynamic start item   
        // and the command ID minus the ID of our root dynamic start item  
        // is less than or equal to the number of projects in the solution.  
        return (commandId >= (int)DynamicMenuPackageGuids.cmdidMyCommand) && ((commandId - (int)DynamicMenuPackageGuids.cmdidMyCommand) < dte2.Solution.Projects.Count);  
    }  
    ```  
  
## <a name="setting-the-vspackage-to-load-only-when-a-solution-has-multiple-projects"></a>设置仅当解决方案包含多个项目时加载 VSPackage  
 因为**设置启动项目**命令没有任何意义，除非活动解决方案具有多个项目，您可以设置你的 VSPackage，若要仅在这种情况下自动加载。 您使用<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>UI 上下文以及<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids.SolutionHasMultipleProjects>。 在 DynamicMenuPackage.cs 文件到 DynamicMenuPackage 类中添加以下属性：  
  
```csharp  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]  
[ProvideMenuResource("Menus.ctmenu", 1)]  
[ProvideAutoLoad(UIContextGuids.SolutionHasMultipleProjects)]  
[Guid(DynamicMenuPackageGuids.PackageGuidString)]  
public sealed class DynamicMenuItemsPackage : Package  
{}  
```  
  
## <a name="testing-the-set-startup-project-command"></a>测试设置启动项目命令  
 现在，你可以测试你的代码。  
  
1. 生成项目并启动调试。 应显示在实验实例。  
  
2. 在实验实例中，打开具有多个项目的解决方案。  
  
     上看到的箭头图标**解决方案资源管理器**工具栏。 在展开它时，应显示表示解决方案中的不同项目的菜单项。  
  
3. 选中的项目之一，它将成为启动项目。  
  
4. 当你关闭解决方案，或打开具有只有一个项目的解决方案时，应会消失的工具栏图标。  
  
## <a name="see-also"></a>请参阅  
 [命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)   
 [VSPackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
