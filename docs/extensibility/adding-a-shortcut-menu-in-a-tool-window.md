---
title: 在工具窗口中添加快捷菜单 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- context menus, adding to tool windows
- menus, context menus
- shortcut menus, adding to tool windows
- tool windows, adding context menus
ms.assetid: 50234537-9e95-4b7e-9cb7-e5cf26d6e9d2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa8d6f5c47289e66a51653e39d31890f09e8ceb2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85904197"
---
# <a name="add-a-shortcut-menu-in-a-tool-window"></a>在工具窗口中添加快捷菜单
本演练将快捷菜单放置在工具窗口中。 快捷菜单是在用户右键单击按钮、文本框或窗口背景时显示的菜单。 快捷菜单上的命令与其他菜单或工具栏上的命令具有相同的行为。 若要支持快捷菜单，请在 *.vsct* 文件中指定它并显示，以响应鼠标右键单击。

工具窗口由继承自的自定义工具窗口类中的 WPF 用户控件组成 <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> 。

本演练演示如何通过在 *.vsct* 文件中声明菜单项，然后使用托管包框架在定义该工具窗口的类中实现它们，将快捷菜单创建为 Visual Studio 菜单。 此方法可促进对 Visual Studio 命令、UI 元素和自动化对象模型的访问。

或者，如果快捷菜单不会访问 Visual Studio 功能，则可以 <xref:System.Windows.FrameworkElement.ContextMenu%2A> 在用户控件中使用 XAML 元素的属性。 有关详细信息，请参阅 [ContextMenu](/dotnet/framework/wpf/controls/contextmenu)。

## <a name="prerequisites"></a>先决条件
从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-the-tool-window-shortcut-menu-package"></a>创建工具窗口快捷菜单包

1. 创建一个名为的 VSIX 项目 `TWShortcutMenu` ，并向其添加一个名为 **快捷菜单** 的工具窗口模板。 有关创建工具窗口的详细信息，请参阅 [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="specifying-the-shortcut-menu"></a>指定快捷菜单
此演练中所示的快捷菜单使用户能够从用于填充工具窗口背景的颜色列表中进行选择。

1. 在 *ShortcutMenuPackage .vsct*中，在名为 GuidShortcutMenuPackageCmdSet 的 GuidSymbol 元素中查找，并声明快捷菜单、快捷菜单组和菜单选项。 GuidSymbol 元素现在应如下所示：

    ```xml
    <GuidSymbol name="guidShortcutMenuPackageCmdSet" value="{00000000-0000-0000-0000-0000}"> // your GUID here
        <IDSymbol name="ShortcutMenuCommandId" value="0x0100" />
        <IDSymbol name="ColorMenu" value="0x1000"/>
        <IDSymbol name="ColorGroup" value="0x1100"/>
        <IDSymbol name="cmdidRed" value="0x102"/>
        <IDSymbol name="cmdidYellow" value="0x103"/>
        <IDSymbol name="cmdidBlue" value="0x104"/>
    </GuidSymbol>
    ```

2. 在 "按钮" 元素之前，创建 "菜单" 元素，然后在其中定义快捷菜单。

    ```vb
    <Menus>
      <Menu guid="guidShortcutMenuPackageCmdSet" id="ColorMenu" type="Context">
        <Strings>
          <ButtonText>Color change</ButtonText>
          <CommandName>ColorChange</CommandName>
        </Strings>
      </Menu>
    </Menus>
    ```

    快捷菜单不具有父项，因为它不是菜单或工具栏的一部分。

3. 创建一个组元素，其中包含包含快捷菜单项的组元素，并将该组与快捷菜单相关联。

    ```xml
    <Groups>
        <Group guid="guidShortcutMenuPackageCmdSet" id="ColorGroup">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorMenu"/>
        </Group>
    </Groups>
    ```

4. 在 "按钮" 元素中，定义将显示在快捷菜单上的各个命令。 按钮元素应如下所示：

    ```xml
    <Buttons>
        <Button guid="guidShortcutMenuPackageCmdSet" id="ShortcutMenuCommandId" priority="0x0100" type="Button">
            <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
            <Icon guid="guidImages" id="bmpPic1" />
            <Strings>
                <ButtonText>ShortcutMenu</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidRed" priority="1" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Red</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidYellow" priority="3" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Yellow</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidBlue" priority="5" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Blue</ButtonText>
            </Strings>
        </Button>
    </Buttons>
    ```

5. 在 *ShortcutMenuCommand.cs*中，添加命令集 GUID、快捷菜单和菜单项的定义。

    ```csharp
    public const string guidShortcutMenuPackageCmdSet = "00000000-0000-0000-0000-00000000"; // your GUID will differ
    public const int ColorMenu = 0x1000;
    public const int cmdidRed = 0x102;
    public const int cmdidYellow = 0x103;
    public const int cmdidBlue = 0x104;
    ```

    这些是在 *ShortcutMenuPackage* 文件的 "符号" 部分中定义的命令 id。 此处不包含上下文组，因为它仅在 *.vsct* 文件中是必需的。

## <a name="implementing-the-shortcut-menu"></a>实现快捷菜单
 本部分实现快捷菜单及其命令。

1. 在 *ShortcutMenu.cs*中，工具窗口可以获取菜单命令服务，但它包含的控件不能。 以下步骤演示如何使 menu 命令服务可用于用户控件。

2. 在 *ShortcutMenu.cs*中，添加以下 using 指令：

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    ```

3. 重写工具窗口的 Initialize ( # A1 方法，以获取菜单命令服务并添加控件，并将菜单命令服务传递给构造函数：

    ```csharp
    protected override void Initialize()
    {
        var commandService = (OleMenuCommandService)GetService(typeof(IMenuCommandService));
        Content = new ShortcutMenuControl(commandService);
    }
    ```

4. 在快捷菜单中，删除添加控件的行。 构造函数现在应如下所示：

    ```csharp
    public ShortcutMenu() : base(null)
    {
        this.Caption = "ShortcutMenu";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
    }
    ```

5. 在 *ShortcutMenuControl.xaml.cs*中，为 menu 命令服务添加私有字段，并更改控制构造函数以采用菜单命令服务。 然后使用菜单命令服务添加上下文菜单命令。 ShortcutMenuControl 构造函数现在应类似于以下代码。 稍后将定义该命令处理程序。

    ```csharp
    public ShortcutMenuControl(OleMenuCommandService service)
    {
        this.InitializeComponent();
        commandService = service;

        if (null !=commandService)
        {
            // Create an alias for the command set guid.
            Guid guid = new Guid(ShortcutMenuCommand.guidShortcutMenuPackageCmdSet);

            // Create the command IDs.
            var red = new CommandID(guid, ShortcutMenuCommand.cmdidRed);
            var yellow = new CommandID(guid, ShortcutMenuCommand.cmdidYellow);
            var blue = new CommandID(guid, ShortcutMenuCommand.cmdidBlue);

            // Add a command for each command ID.
            commandService.AddCommand(new MenuCommand(ChangeColor, red));
            commandService.AddCommand(new MenuCommand(ChangeColor, yellow));
            commandService.AddCommand(new MenuCommand(ChangeColor, blue));
        }
    }
    ```

6. 在 *ShortcutMenuControl*中，将事件添加 <xref:System.Windows.UIElement.MouseRightButtonDown> 到顶级 <xref:System.Windows.Controls.UserControl> 元素。 XAML 文件现在应如下所示：

    ```vb
    <UserControl x:Class="TWShortcutMenu.ShortcutMenuControl"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            Background="{DynamicResource VsBrush.Window}"
            Foreground="{DynamicResource VsBrush.WindowText}"
            mc:Ignorable="d"
            d:DesignHeight="300" d:DesignWidth="300"
            Name="MyToolWindow"
            MouseRightButtonDown="MyToolWindow_MouseRightButtonDown">
        <Grid>
            <StackPanel Orientation="Vertical">
                <TextBlock Margin="10" HorizontalAlignment="Center">ShortcutMenu</TextBlock>
            </StackPanel>
        </Grid>
    </UserControl>
    ```

7. 在 *ShortcutMenuControl.xaml.cs*中，为事件处理程序添加存根。

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
    . . .
    }
    ```

8. 将以下 using 指令添加到同一个文件中：

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    using System;
    using System.Windows.Input;
    using System.Windows.Media;
    ```

9. `MyToolWindowMouseRightButtonDown`按如下所示实现事件。

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
        if (null != commandService)
        {
            CommandID menuID = new CommandID(
                new Guid(ShortcutMenuCommand.guidShortcutMenuPackageCmdSet),
                ShortcutMenuCommand.ColorMenu);
            Point p = this.PointToScreen(e.GetPosition(this));
            commandService.ShowContextMenu(menuID, (int)p.X, (int)p.Y);
        }
    }
    ```

    这 <xref:System.ComponentModel.Design.CommandID> 会为快捷菜单创建一个对象，标识鼠标单击的位置，并使用方法打开该位置中的快捷菜单 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService.ShowContextMenu%2A> 。

10. 实现命令处理程序。

    ```csharp
    private void ChangeColor(object sender, EventArgs e)
    {
        var mc = sender as MenuCommand;

        switch (mc.CommandID.ID)
        {
            case ShortcutMenuCommand.cmdidRed:
                MyToolWindow.Background = Brushes.Red;
                break;
            case ShortcutMenuCommand.cmdidYellow:
                MyToolWindow.Background = Brushes.Yellow;
                break;
            case ShortcutMenuCommand.cmdidBlue:
                MyToolWindow.Background = Brushes.Blue;
                break;
        }
    }
    ```

    在这种情况下，只有一个方法通过标识 <xref:System.ComponentModel.Design.CommandID> 并相应地设置背景色来处理所有菜单项的事件。 如果菜单项包含不相关的命令，您将为每个命令创建一个单独的事件处理程序。

## <a name="test-the-tool-window-features"></a>测试工具窗口功能

1. 生成项目并启动调试。 这将显示实验实例。

2. 在实验实例中，单击 " **视图"/"其他窗口**"，然后单击 " **快捷菜单**"。 执行此操作应显示工具窗口。

3. 右键单击工具窗口的 "正文"。 应显示具有颜色列表的快捷菜单。

4. 单击快捷菜单上的颜色。 工具窗口的背景色应更改为所选颜色。

## <a name="see-also"></a>另请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
- [使用和提供服务](../extensibility/using-and-providing-services.md)
