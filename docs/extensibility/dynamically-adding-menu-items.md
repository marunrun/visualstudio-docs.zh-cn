---
title: 动态添加菜单项 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- DYNAMICITEMSTART
- menu items, adding dynamically
- menus, adding dynamic items
ms.assetid: d281e9c9-b289-4d64-8d0a-094bac6c333c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4387c1930e09e49c0ec5c36ccedc1bb83dc273f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712058"
---
# <a name="dynamically-add-menu-items"></a>动态添加菜单项
通过在 Visual Studio 命令表`DynamicItemStart`*（.vsct*） 文件中的占位符按钮定义上指定命令标志，然后定义（以代码形式）显示和处理命令的菜单项数，可以在运行时添加菜单项。 加载 VSPackage 时，占位符将替换为动态菜单项。

 Visual Studio 使用 **"最近使用**（MRU）"列表中的动态列表（显示最近打开的文档的名称）和显示当前打开的窗口名称的**Windows**列表。   命令`DynamicItemStart`定义上的标志指定命令是占位符，直到打开 VSPackage。 打开 VSPackage 时，占位符将被在运行时创建并添加到动态列表中的 0 个或多个命令替换。 在打开 VSPackage 之前，您可能无法看到显示动态列表的菜单上的位置。  要填充动态列表，Visual Studio 要求 VSPackage 查找具有 ID 的命令，该命令的第一个字符与占位符的 ID 相同。 当 Visual Studio 找到匹配命令时，它将该命令的名称添加到动态列表中。 然后，它增加 ID 并查找另一个匹配的命令添加到动态列表中，直到没有更多的动态命令。

 本演练演示如何使用**解决方案资源管理器**工具栏上的命令在 Visual Studio 解决方案中设置启动项目。 它使用菜单控制器，该菜单控制器具有活动解决方案中项目的动态下拉列表。 为了防止在未打开解决方案或打开的解决方案只有一个项目时出现此命令，仅当解决方案有多个项目时才加载 VSPackage。

 有关 *.vsct*文件的详细信息，请参阅[可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

## <a name="create-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展

1. 创建名为 的`DynamicMenuItems`VSIX 项目。

2. 打开项目时，添加自定义命令项模板并将其命名为**DynamicMenu**。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="setting-up-the-elements-in-the-vsct-file"></a>设置 *.vsct*文件中的元素
 要创建工具栏上具有动态菜单项的菜单控制器，请指定以下元素：

- 两个命令组，一个包含菜单控制器，另一个包含下拉菜单项

- 一个类型的菜单元素`MenuController`

- 两个按钮，一个充当菜单项的占位符，另一个提供工具栏上的图标和工具提示。

1. 在*动态菜单包.vsct 中*，定义命令指示。 转到"符号"部分并替换**guidDynamicMenu 包装 CmdSet** GuidSymbol 块中的 IDSymbol 元素。 您需要为两个组（菜单控制器、占位符命令和锚点命令）定义 IDSymbol 元素。

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

2. 在"组"部分中，删除现有组并添加刚刚定义的两个组：

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

     添加菜单控制器。 设置动态可见性命令标志，因为它并不总是可见的。 不显示按钮文本。

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

3. 添加两个按钮，一个作为动态菜单项的占位符，一个作为菜单控制器的锚点。

     占位符按钮的父级是**MyMenuControllerGroup。** 将动态项目启动、动态可见性和文本更改命令标志添加到占位符按钮。 不显示按钮文本。

     锚点按钮包含图标和工具提示文本。 锚点按钮的父级也是**MyMenu 控制器组**。 添加 NoShowOnMenu 控制器命令标志，以确保按钮实际上不会出现在菜单控制器下拉列表中，以及固定菜单控制器命令标志使其成为永久锚点。

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

4. 向项目添加图标（在 *"资源"* 文件夹中），然后在 *.vsct*文件中添加对项目的引用。 在本演练中，我们使用项目模板中包含的箭头图标。

5. 在"符号"部分之前"命令"部分之外添加可见性约束部分。 （如果在符号之后添加，您可能会收到警告。此部分确保菜单控制器仅在加载具有多个项目的解决方案时才出现。

    ```xml
    <VisibilityConstraints>
         <!--Make the MenuController show up only when there is a solution with more than one project loaded-->
        <VisibilityItem guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" context="UICONTEXT_SolutionHasMultipleProjects"/>
    </VisibilityConstraints>
    ```

## <a name="implement-the-dynamic-menu-command"></a>实现动态菜单命令
 创建从<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>继承的动态菜单命令类。 在此实现中，构造函数指定用于匹配命令的谓词。 必须重写<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A>方法以使用此谓词来设置<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A>属性，该属性标识要调用的命令。

1. 创建名为*DynamicItemMenuCommand.cs*的新 C# 类文件，并添加一个名为**DynamicItemMenu命令**的<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>类，该文件从 继承于 ：

    ```csharp
    class DynamicItemMenuCommand : OleMenuCommand
    {

    }

    ```

2. 添加以下 using 指令：

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    using System.ComponentModel.Design;
    ```

3. 添加专用字段以存储匹配谓词：

    ```csharp
    private Predicate<int> matches;

    ```

4. 添加从构造函数继承的<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>构造函数，并指定命令处理程序和<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>处理程序。 添加用于匹配命令的谓词：

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

5. 重写<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A>方法，以便调用匹配谓词并设置<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A>属性：

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
 动态菜单构造函数是设置菜单命令的位置，包括动态菜单和菜单项。

1. 在*DynamicMenuPackage.cs*中，添加命令集的 GUID 和命令 ID：

    ```csharp
    public const string guidDynamicMenuPackageCmdSet = "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    public const uint cmdidMyCommand = 0x104;
    ```

2. 在*DynamicMenu.cs*文件中，添加以下使用指令：

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using System.ComponentModel.Design;
    ```

3. 在`DynamicMenu`类中，添加专用字段**dte2**。

    ```csharp
    private DTE2 dte2;
    ```

4. 添加专用根项目 Id 字段：

    ```csharp
    private int rootItemId = 0;
    ```

5. 在动态菜单构造函数中，添加菜单命令。 在下一节中，我们将定义命令处理程序、`BeforeQueryStatus`事件处理程序和匹配谓词。

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
 要在菜单控制器上实现动态菜单项，必须在单击动态项时处理该命令。 还必须实现设置菜单项状态的逻辑。 将处理程序添加到类`DynamicMenu`。

1. 要实现 **"设置启动项目"** 命令，添加**OnIn 被调用的 DynamicItem**事件处理程序。 它查找名称与已调用的命令的文本相同的项目，并通过在<xref:EnvDTE.SolutionBuild.StartupProjects%2A>属性中设置其绝对路径将其设置为启动项目。

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

2. 添加事件`OnBeforeQueryStatusDynamicItem`处理程序。 这是在事件之前调用的`QueryStatus`处理程序。 它确定菜单项是否为"实际"项，即不是占位符项，以及该项目是否已选中（这意味着项目已设置为启动项目）。

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

现在实现匹配谓词。 我们需要确定两件事：第一，命令 ID 是否有效（它大于或等于声明的命令 ID），第二，它是否指定了可能的项目（它小于解决方案中的项目数）。

```csharp
private bool IsValidDynamicItem(int commandId)
{
    // The match is valid if the command ID is >= the id of our root dynamic start item
    // and the command ID minus the ID of our root dynamic start item
    // is less than or equal to the number of projects in the solution.
    return (commandId >= (int)DynamicMenuPackageGuids.cmdidMyCommand) && ((commandId - (int)DynamicMenuPackageGuids.cmdidMyCommand) < dte2.Solution.Projects.Count);
}
```

## <a name="set-the-vspackage-to-load-only-when-a-solution-has-multiple-projects"></a>将 VS 包设置为仅在解决方案具有多个项目时加载
 由于 **"设置启动项目"** 命令没有意义，除非活动解决方案有多个项目，因此可以将 VSPackage 设置为仅在该情况下自动加载。 与<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>UI 上下文<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids.SolutionHasMultipleProjects>一起使用。 在*DynamicMenuPackage.cs*文件中向 DynamicMenu 包类添加以下属性：

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
[ProvideMenuResource("Menus.ctmenu", 1)]
[ProvideAutoLoad(UIContextGuids.SolutionHasMultipleProjects)]
[Guid(DynamicMenuPackage.PackageGuidString)]
public sealed class DynamicMenuItemsPackage : Package
{}
```

## <a name="test-the-set-startup-project-command"></a>测试集启动项目命令
 现在，您可以测试代码。

1. 生成项目并启动调试。 应出现实验实例。

2. 在实验实例中，打开一个有多个项目的解决方案。

     您应该在**解决方案资源管理器**工具栏上看到箭头图标。 展开它时，应显示表示解决方案中不同项目的菜单项。

3. 当您检查其中一个项目时，它将成为启动项目。

4. 当您关闭解决方案或打开只有一个项目的解决方案时，工具栏图标应消失。

## <a name="see-also"></a>请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
- [VS包如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
