---
title: 工具窗口中添加快捷菜单 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- context menus, adding to tool windows
- menus, context menus
- shortcut menus, adding to tool windows
- tool windows, adding context menus
ms.assetid: 50234537-9e95-4b7e-9cb7-e5cf26d6e9d2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 36df685197acbac4372daa8f8c813acf22357678
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309939"
---
# <a name="add-a-shortcut-menu-in-a-tool-window"></a>工具窗口中添加快捷菜单
本演练将在工具窗口的快捷菜单。 快捷菜单，在用户右键单击按钮、 文本框中或窗口背景时，将显示一个菜单。 快捷菜单上的命令的行为与其他菜单或工具栏上的命令相同。 若要支持快捷方式菜单上，指定在 *.vsct*文件并将其显示在响应鼠标右键单击。

工具窗口包含 WPF 用户控件继承的自定义工具窗口类中的<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>。

本演练演示如何创建作为 Visual Studio 菜单中，通过声明中的菜单项的快捷菜单 *.vsct*文件，并使用托管包框架来定义工具窗口的类中实现它们。 此方法方便了对 Visual Studio 命令、 UI 元素和自动化对象模型的访问。

或者，如果快捷菜单将不访问 Visual Studio 功能，则可以使用<xref:System.Windows.FrameworkElement.ContextMenu%2A>中的用户控件的 XAML 元素的属性。 有关详细信息，请参阅[ContextMenu](/dotnet/framework/wpf/controls/contextmenu)。

## <a name="prerequisites"></a>系统必备
从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-the-tool-window-shortcut-menu-package"></a>创建工具窗口快捷方式菜单包

1. 创建一个名为的 VSIX 项目`TWShortcutMenu`并添加一个名为的工具窗口模板**快捷菜单**到它。 有关创建工具窗口的详细信息，请参阅[与工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="specifying-the-shortcut-menu"></a>指定的快捷菜单
快捷菜单，如本演练中所示使用户可以从用于填充工具窗口的背景的颜色的列表中选择。

1. 在中*ShortcutMenuPackage.vsct*，名为 guidShortcutMenuPackageCmdSet，GuidSymbol 元素中查找并声明的快捷菜单、 快捷方式菜单组和菜单选项。 GuidSymbol 元素现在应如下所示：

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

2. 之前的按钮元素，创建菜单元素以及然后在其中定义的快捷菜单。

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

    快捷菜单不具有父级，因为它不是菜单或工具栏的一部分。

3. 创建组元素具有一个组元素，包含的快捷菜单项，并将组关联的快捷菜单。

    ```xml
    <Groups>
        <Group guid="guidShortcutMenuPackageCmdSet" id="ColorGroup">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorMenu"/>
        </Group>
    </Groups>
    ```

4. 在按钮元素中，在快捷菜单上定义将显示单个命令。 按钮元素应如下所示：

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

5. 在中*ShortcutMenuCommand.cs*，添加定义，该命令集 GUID、 快捷菜单和菜单项。

    ```csharp
    public const string guidShortcutMenuPackageCmdSet = "00000000-0000-0000-0000-00000000"; // your GUID will differ
    public const int ColorMenu = 0x1000;
    public const int cmdidRed = 0x102;
    public const int cmdidYellow = 0x103;
    public const int cmdidBlue = 0x104;
    ```

    这些是在的 Symbols 部分中定义的相同命令 Id *ShortcutMenuPackage.vsct*文件。 此处的上下文组不包含因为仅在需要它 *.vsct*文件。

## <a name="implementing-the-shortcut-menu"></a>实现的快捷菜单
 本部分中实现的快捷菜单和命令。

1. 在中*ShortcutMenu.cs*，工具窗口可获取菜单命令服务中，但它所包含的控件不能。 以下步骤说明如何使菜单命令服务可用于用户控件。

2. 在中*ShortcutMenu.cs*，添加以下 using 语句：

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    ```

3. 重写工具窗口的 initialize （） 方法以获取菜单命令服务并添加控件，将菜单命令服务传递给构造函数：

    ```csharp
    protected override void Initialize()
    {
        var commandService = (OleMenuCommandService)GetService(typeof(IMenuCommandService));
        Content = new ShortcutMenuControl(commandService);
    }
    ```

4. 在快捷菜单工具窗口构造函数中，删除将控件添加的行。 构造函数现在应如下所示：

    ```csharp
    public ShortcutMenu() : base(null)
    {
        this.Caption = "ShortcutMenu";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
    }
    ```

5. 在中*ShortcutMenuControl.xaml.cs*、 添加菜单命令服务的私有字段和更改控件构造函数来执行菜单命令服务。 然后使用菜单命令服务中添加上下文菜单命令。 ShortcutMenuControl 构造函数现在应如以下代码所示。 命令处理程序将在以后定义。

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

6. 在中*ShortcutMenuControl.xaml*，添加<xref:System.Windows.UIElement.MouseRightButtonDown>到最高级别事件<xref:System.Windows.Controls.UserControl>元素。 XAML 文件现在应如下所示：

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

7. 在中*ShortcutMenuControl.xaml.cs*，添加事件处理程序的存根。

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
    . . .
    }
    ```

8. 将以下代码添加到相同文件 using 语句：

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    using System;
    using System.Windows.Input;
    using System.Windows.Media;
    ```

9. 实现`MyToolWindowMouseRightButtonDown`事件，如下所示。

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

    这将创建<xref:System.ComponentModel.Design.CommandID>快捷菜单中的对象标识的鼠标单击的位置，并通过使用在该位置打开快捷菜单<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService.ShowContextMenu%2A>方法。

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

    在这种情况下，只是一种方法处理的所有菜单项的事件通过标识<xref:System.ComponentModel.Design.CommandID>并相应地设置背景色。 如果菜单项中包含不相关的命令，你将创建一个单独的事件处理程序对于每个命令。

## <a name="test-the-tool-window-features"></a>测试工具窗口功能

1. 生成项目并启动调试。 将显示在实验实例。

2. 在实验实例中，单击**视图 / 其他 Windows**，然后单击**快捷菜单**。 执行此操作应显示在工具窗口。

3. 右键单击工具窗口中的正文中。 应显示有一个颜色列表的快捷菜单。

4. 单击快捷菜单上的颜色。 工具窗口背景颜色应更改为所选颜色。

## <a name="see-also"></a>请参阅
- [命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
- [使用并提供服务](../extensibility/using-and-providing-services.md)
