---
title: 向菜单添加子菜单 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- context menus
- submenus, cascading
- cascading submenus
- menus, creating cascading submenus
ms.assetid: 692600cb-d052-40e2-bdae-4354ae7c6c84
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 59c9364d03aab135f7c9b4bf91df21b949e78ee4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740267"
---
# <a name="add-a-submenu-to-a-menu"></a>向菜单添加子菜单
本演练基于在["向可视化工作室菜单栏添加菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)"中的演示为基础，演示如何向**TestMenu 菜单**添加子菜单。

 子菜单是另一个菜单中显示的辅助菜单。 子菜单可以通过其名称后面的箭头进行标识。 单击名称会导致子菜单及其命令显示。

 本演练在 Visual Studio 菜单栏的菜单中创建一个子菜单，并在子菜单上放置一个新命令。 演练还实现了新命令。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="add-a-submenu-to-a-menu"></a>向菜单添加子菜单

1. 按照向[可视化工作室菜单栏添加菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)中的步骤创建项目和菜单项。 本演练中的步骤假定 VSIX 项目的名称为`TopLevelMenu`。

2. 打开*测试命令包.vsct*. 在本节`<Symbols>`中，为子`<IDSymbol>`菜单添加一个元素，为子菜单组添加一个元素，为命令添加一个元素，`<GuidSymbol>`所有这些元素都在名为"guidTopLevelMenuCmdSet"的节点中。 这是包含顶级菜单`<IDSymbol>`元素的同一节点。

    ```xml
    <IDSymbol name="SubMenu" value="0x1100"/>
    <IDSymbol name="SubMenuGroup" value="0x1150"/>
    <IDSymbol name="cmdidTestSubCommand" value="0x0105"/>
    ```

3. 将新创建的子菜单添加到节中`<Menus>`。

    ```xml
    <Menu guid="guidTestCommandPackageCmdSet" id="SubMenu" priority="0x0100" type="Menu">
        <Parent guid="guidTestCommandPackageCmdSet" id="MyMenuGroup"/>
        <Strings>
            <ButtonText>Sub Menu</ButtonText>
            <CommandName>Sub Menu</CommandName>
        </Strings>
    </Menu>
    ```

     父组的 GUID/ID 对指定在["向可视化工作室菜单栏添加菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)"中生成的菜单组，并且是顶级菜单的子级。

4. 将步骤 2 中定义的菜单组添加到`<Groups>`分区，使其成为子菜单的子菜单的子菜单。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" priority="0x0000">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

5. 向`<Buttons>`节添加新`<Button>`元素，将步骤 2 中创建的命令定义为子菜单上的项。

    ```xml
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidTestSubCommand" priority="0x0000" type="Button">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <Strings>
           <CommandName>cmdidTestSubCommand</CommandName>
           <ButtonText>Test Sub Command</ButtonText>
        </Strings>
    </Button>
    ```

6. 生成解决方案并启动调试。 您应该会看到实验实例。

7. 单击 **"测试菜单**"以查看名为 **"子菜单"的新子菜单**。 单击 **"子菜单**"打开子菜单并查看新命令 **"测试子命令**"。 请注意，单击 **"测试子命令**"不执行任何操作。

## <a name="add-a-command"></a>添加命令

1. 打开*TestCommand.cs，* 并在现有命令 ID 之后添加以下命令 ID。

    ```csharp
    public const int cmdidTestSubCmd = 0x0105;
    ```

2. 添加子命令。 查找命令构造函数。 在调用`AddCommand`方法后添加以下行。

    ```csharp
    CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
    MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
    commandService.AddCommand(subItem);
    ```

    稍后将`SubItemCallback`定义命令处理程序。 构造函数现在应如下所示：

    ```csharp
    private TestCommand(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            var menuCommandID = new CommandID(CommandSet, CommandId);
            var menuItem = new MenuCommand(this.MenuItemCallback, menuCommandID);
            commandService.AddCommand(menuItem);

            CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
            MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
            commandService.AddCommand(subItem);
        }
    }
    ```

3. 添加 `SubItemCallback()`。 这是单击子菜单中的新命令时调用的方法。

    ```csharp
    private void SubItemCallback(object sender, EventArgs e)
    {
        IVsUIShell uiShell = (IVsUIShell)this.ServiceProvider.GetServiceAsync(typeof(SVsUIShell));
        Guid clsid = Guid.Empty;
        int result;
        uiShell.ShowMessageBox(
            0,
            ref clsid,
            "TestCommand",
            string.Format(CultureInfo.CurrentCulture,
            "Inside TestCommand.SubItemCallback()",
            this.ToString()),
            string.Empty,
            0,
            OLEMSGBUTTON.OLEMSGBUTTON_OK,
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
            OLEMSGICON.OLEMSGICON_INFO,
            0,
            out result);
    }
    ```

4. 生成项目并启动调试。 应出现实验实例。

5. 在 **"测试菜单"** 菜单上，单击 **"子菜单**"，然后单击 **"测试子命令**"。 应显示一个消息框并显示文本"测试命令内部测试命令.子项目回调（）"。

## <a name="see-also"></a>请参阅

- [向视觉工作室菜单栏添加菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
