---
title: 向菜单中添加子菜单 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: cb143a611b1fb1f4278d28fdf9423a1f6613a68d
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904184"
---
# <a name="add-a-submenu-to-a-menu"></a>向菜单中添加子菜单
本演练基于将菜单添加到[Visual Studio 菜单栏](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)中的演示，通过显示如何将子菜单添加到 " **TestMenu** " 菜单来构建。

 子菜单是在另一个菜单中显示的辅助菜单。 子菜单可以通过其名称后面的箭头进行标识。 单击该名称会显示子菜单及其命令。

 本演练将在 Visual Studio 菜单栏上的菜单中创建一个子菜单，并在子菜单中放置一个新命令。 本演练还实现了新的命令。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="add-a-submenu-to-a-menu"></a>向菜单中添加子菜单

1. 按照[将菜单添加到 Visual Studio 菜单栏](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)中的步骤创建项目和菜单项。 本演练中的步骤假定 VSIX 项目的名称为 `TopLevelMenu` 。

2. 打开*TestCommandPackage. .vsct*。 在部分中，为子 `<Symbols>` 菜单添加一个 `<IDSymbol>` 元素，为子菜单组添加一个元素，并在名为 "guidTopLevelMenuCmdSet" 的节点中添加一个元素 `<GuidSymbol>` 。 此节点与包含顶级菜单的元素的节点相同 `<IDSymbol>` 。

    ```xml
    <IDSymbol name="SubMenu" value="0x1100"/>
    <IDSymbol name="SubMenuGroup" value="0x1150"/>
    <IDSymbol name="cmdidTestSubCommand" value="0x0105"/>
    ```

3. 将新创建的子菜单添加到 `<Menus>` 部分。

    ```xml
    <Menu guid="guidTestCommandPackageCmdSet" id="SubMenu" priority="0x0100" type="Menu">
        <Parent guid="guidTestCommandPackageCmdSet" id="MyMenuGroup"/>
        <Strings>
            <ButtonText>Sub Menu</ButtonText>
            <CommandName>Sub Menu</CommandName>
        </Strings>
    </Menu>
    ```

     父对象的 GUID/ID 对指定在[向 Visual Studio 菜单栏添加菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)中生成的菜单组，并且是顶级菜单的子菜单。

4. 将在步骤2中定义的菜单组添加到 `<Groups>` 部分，并使其成为子菜单的子菜单。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" priority="0x0000">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

5. 向部分添加一个新 `<Button>` 元素 `<Buttons>` ，以将步骤2中创建的命令定义为子菜单上的一项。

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

6. 生成解决方案并启动调试。 应会看到实验实例。

7. 单击 " **TestMenu** "，以查看名为 "**子菜单**" 的新子菜单。 单击 "**子菜单**" 打开子菜单，并查看新的 "**测试子命令**" 命令。 请注意，单击 "**测试子命令**" 不执行任何操作。

## <a name="add-a-command"></a>添加命令

1. 打开*TestCommand.cs* ，并在现有命令 id 后面添加以下命令 id。

    ```csharp
    public const int cmdidTestSubCmd = 0x0105;
    ```

2. 添加子命令。 找到命令构造函数。 在调用方法之后，添加以下行 `AddCommand` 。

    ```csharp
    CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
    MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
    commandService.AddCommand(subItem);
    ```

    `SubItemCallback`稍后将定义该命令处理程序。 构造函数现在应如下所示：

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

4. 生成项目并启动调试。 应显示实验实例。

5. 在 " **TestMenu** " 菜单上，单击 "**子菜单**"，然后单击 "**测试子命令**"。 将出现一个消息框，并显示 "Testcommand (. SubItemCallback （）中的测试命令" 文本。

## <a name="see-also"></a>另请参阅

- [将菜单添加到 Visual Studio 菜单栏](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
