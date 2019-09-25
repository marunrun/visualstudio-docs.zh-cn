---
title: 动态添加菜单项 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- DYNAMICITEMSTART
- menu items, adding dynamically
- menus, adding dynamic items
ms.assetid: d281e9c9-b289-4d64-8d0a-094bac6c333c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 136ee925f1ee7505e7058eb643d7bac3a9222c06
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71252365"
---
# <a name="dynamically-add-menu-items"></a>动态添加菜单项
你可以在运行时添加菜单项，方法是`DynamicItemStart`在 Visual Studio 命令表（ *.vsct*）文件中的占位符按钮定义上指定命令标志，然后定义（在代码中）要显示和处理命令的菜单项的数目。 加载 VSPackage 时，会将占位符替换为动态菜单项。

 Visual Studio 在**最近使用**的（MRU）列表中使用动态列表，该列表显示最近打开的文档的名称和**windows**列表，其中显示当前打开的窗口的名称。   命令`DynamicItemStart`定义上的标志指定在 VSPackage 打开之前，该命令是占位符。 打开 VSPackage 后，占位符将被替换为0个或多个在运行时创建并添加到动态列表中的命令。 在打开 VSPackage 之前，你可能无法在菜单上看到显示动态列表的位置。  为了填充动态列表，Visual Studio 会要求 VSPackage 查找 ID 的命令，该命令的第一个字符与占位符的 ID 相同。 当 Visual Studio 查找匹配的命令时，它会将命令的名称添加到动态列表。 然后，它会递增 ID 并查找另一个匹配的命令，以将其添加到动态列表，直到没有更多动态命令。

 本演练演示如何在 Visual Studio 解决方案中使用**解决方案资源管理器**工具栏上的命令来设置启动项目。 它使用具有活动解决方案中项目的动态下拉列表的菜单控制器。 若要使此命令在没有打开解决方案时显示，或当打开的解决方案只有一个项目时显示，VSPackage 仅在解决方案有多个项目时才会加载。

 有关 *.vsct*文件的详细信息，请参阅[Visual Studio 命令表（.vsct）文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

## <a name="create-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展

1. 创建一个名为`DynamicMenuItems`的 VSIX 项目。

2. 当项目打开时，添加一个自定义命令项模板并将其命名为**DynamicMenu**。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="setting-up-the-elements-in-the-vsct-file"></a>设置 *.vsct*文件中的元素
 若要在工具栏上创建具有动态菜单项的菜单控制器，请指定以下元素：

- 两个命令组，一个包含菜单控制器，另一个包含下拉列表中的菜单项

- 类型的一个菜单元素`MenuController`

- 两个按钮，一个用于作为菜单项的占位符，另一个用于提供工具栏上的图标和工具提示。

1. 在*DynamicMenuPackage. .vsct*中，定义命令 id。 中转到符号部分并替换**guidDynamicMenuPackageCmdSet** GuidSymbol 块中的 IDSymbol 元素。 需要为两个组、菜单控制器、占位符命令和定位点命令定义 IDSymbol 元素。

    ```xml
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

2. 在 "组" 部分中，删除现有组并添加刚才定义的两个组：

    ```xml
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

     添加 MenuController。 设置 DynamicVisibility 命令标志，因为它并非始终可见。 ButtonText 不会显示。

    ```xml
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

3. 添加两个按钮，一个用于动态菜单项的占位符，另一个用作 MenuController 的定位点。

     占位符按钮的父项为**MyMenuControllerGroup**。 将 DynamicItemStart、DynamicVisibility 和 TextChanges 命令标志添加到占位符按钮。 ButtonText 不会显示。

     定位点按钮包含图标和工具提示文本。 定位点按钮的父项也是**MyMenuControllerGroup**。 添加 NoShowOnMenuController 命令标志，以确保按钮不会真正出现在 "菜单控制器" 下拉列表中，并通过 FixMenuController 命令标志将其设为永久定位。

    ```xml
    <!-- The placeholder for the dynamic items that expand to N items at run time. -->
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

4. 将图标添加到项目（在*Resources*文件夹中），然后在 *.vsct*文件中添加对它的引用。 在本演练中，我们使用项目模板中包含的 "箭头" 图标。

5. 将 VisibilityConstraints 节添加到 "命令" 部分的紧靠符号部分之前。 （如果在符号后面添加它，则可能会收到警告。）本部分确保仅当加载包含多个项目的解决方案时，才会显示菜单控制器。

    ```xml
    <VisibilityConstraints>
         <!--Make the MenuController show up only when there is a solution with more than one project loaded-->
        <VisibilityItem guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" context="UICONTEXT_SolutionHasMultipleProjects"/>
    </VisibilityConstraints>
    ```

## <a name="implement-the-dynamic-menu-command"></a>实现动态菜单命令
 创建一个从<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>继承的动态菜单命令类。 在此实现中，构造函数指定用于匹配命令的谓词。 必须重写<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A>方法，以便使用此谓词来<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A>设置属性，该属性用于标识要调用的命令。

1. 创建名为C# *DynamicItemMenuCommand.cs*的新类文件，并添加一个从 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand>继承的名为 DynamicItemMenuCommand 的类：

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

3. 添加私有字段以存储 match 谓词：

    ```csharp
    private Predicate<int> matches;

    ```

4. 添加从<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>构造函数继承的构造函数，并指定命令处理程序<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>和处理程序。 添加用于匹配命令的谓词：

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

5. 重写<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A>方法，使其调用匹配谓词并设置属性： <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A>

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

## <a name="add-the-command"></a>添加命令
 在 DynamicMenu 构造函数中，可以设置菜单命令，包括动态菜单和菜单项。

1. 在*DynamicMenuPackage.cs*中，添加命令集的 GUID 和命令 ID：

    ```csharp
    public const string guidDynamicMenuPackageCmdSet = "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    public const uint cmdidMyCommand = 0x104;
    ```

2. 在*DynamicMenu.cs*文件中，添加以下 using 语句：

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using System.ComponentModel.Design;
    ```

3. 在类中，添加私有字段**dte2。** `DynamicMenu`

    ```csharp
    private DTE2 dte2;
    ```

4. 添加专用 rootItemId 字段：

    ```csharp
    private int rootItemId = 0;
    ```

5. 在 DynamicMenu 构造函数中，添加菜单命令。 在下一部分中，我们将定义命令处理程序、 `BeforeQueryStatus`事件处理程序和匹配谓词。

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

## <a name="implement-the-handlers"></a>实现处理程序
 若要在菜单控制器上实现动态菜单项，则必须在单击动态项时处理该命令。 还必须实现逻辑来设置菜单项的状态。 将处理程序添加到`DynamicMenu`类。

1. 若要实现 "**设置启动项目**" 命令，请添加**OnInvokedDynamicItem**事件处理程序。 它会查找名称与已调用命令的文本相同的项目，并将其设置为启动项目，方法是在<xref:EnvDTE.SolutionBuild.StartupProjects%2A>属性中设置其绝对路径。

    ```csharp
    private void OnInvokedDynamicItem(object sender, EventArgs args)
    {
        DynamicItemMenuCommand invokedCommand = (DynamicItemMenuCommand)sender;
        // If the command is already checked, we don't need to do anything
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

2. `OnBeforeQueryStatusDynamicItem`添加事件处理程序。 这是在`QueryStatus`事件之前调用的处理程序。 它确定菜单项是否为 "真实" 项（即不是占位符项），以及该项是否已被选中（这意味着项目已设置为启动项目）。

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

## <a name="implement-the-command-id-match-predicate"></a>实现命令 ID 匹配谓词

现在实现 match 谓词。 我们需要确定两项内容：首先，命令 ID 是否有效（它大于或等于声明的命令 ID），第二种是指定可能的项目（它小于解决方案中项目的数目）。

```csharp
private bool IsValidDynamicItem(int commandId)
{
    // The match is valid if the command ID is >= the id of our root dynamic start item
    // and the command ID minus the ID of our root dynamic start item
    // is less than or equal to the number of projects in the solution.
    return (commandId >= (int)DynamicMenuPackageGuids.cmdidMyCommand) && ((commandId - (int)DynamicMenuPackageGuids.cmdidMyCommand) < dte2.Solution.Projects.Count);
}
```

## <a name="set-the-vspackage-to-load-only-when-a-solution-has-multiple-projects"></a>将 VSPackage 设置为仅在解决方案有多个项目时加载
 因为除非活动解决方案包含多个项目，否则 "**设置启动项目**" 命令没有意义，因此，你可以将 VSPackage 设置为仅在这种情况下自动加载。 将与<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> UI 上下文<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids.SolutionHasMultipleProjects>一起使用。 在*DynamicMenuPackage.cs*文件中，将以下属性添加到 DynamicMenuPackage 类：

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
[ProvideMenuResource("Menus.ctmenu", 1)]
[ProvideAutoLoad(UIContextGuids.SolutionHasMultipleProjects)]
[Guid(DynamicMenuPackage.PackageGuidString)]
public sealed class DynamicMenuItemsPackage : Package
{}
```

## <a name="test-the-set-startup-project-command"></a>测试 "设置启动项目" 命令
 现在可以测试代码了。

1. 生成项目并启动调试。 应显示实验实例。

2. 在实验实例中，打开包含多个项目的解决方案。

     **解决方案资源管理器**工具栏上应会显示箭头图标。 展开此项时，将显示表示解决方案中不同项目的菜单项。

3. 选中其中一个项目时，它将成为启动项目。

4. 关闭解决方案或打开只包含一个项目的解决方案时，工具栏图标应会消失。

## <a name="see-also"></a>请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
- [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)