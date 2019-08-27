---
title: 将菜单控制器添加到工具栏 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding menu controllers
- menus, adding menu controllers to toolbars
- menu controllers, adding to toolbars
ms.assetid: 6af9b0b4-037f-404c-bb40-aaa1970768ea
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: eaa53a9bf8d33ad145d75bdb2d72e6820f806711
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349800"
---
# <a name="add-a-menu-controller-to-a-toolbar"></a>将菜单控制器添加到工具栏
本演练基于[将工具栏添加到工具窗口](../extensibility/adding-a-toolbar-to-a-tool-window.md)演练，并演示如何将菜单控制器添加到工具窗口工具栏。 如下所示的步骤还可应用于在中创建工具栏[将工具栏添加](../extensibility/adding-a-toolbar.md)演练。

菜单控制器是拆分控件。 左侧和右侧的菜单控制器显示上次使用的命令，并可以通过单击运行它。 右侧的菜单控制器是一个箭头，单击，将打开的其他命令的列表。 当单击上列表中，命令运行的命令，它取代了左侧和右侧的菜单控制器上的命令。 在这种方式，菜单控制器运行，类似于始终显示列表中的上次使用的命令的命令按钮。

菜单控制器可以出现在菜单上，但它们最常使用工具栏上。

## <a name="prerequisites"></a>系统必备
从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-menu-controller"></a>创建菜单控制器

1. 请按照中所述的过程[将工具栏添加到工具窗口](../extensibility/adding-a-toolbar-to-a-tool-window.md)若要创建一个工具窗口，有一个工具栏。

2. 在中*TWTestCommandPackage.vsct*，请转到符号部分。 在名为的 GuidSymbol 元素**guidTWTestCommandPackageCmdSet**，声明菜单控制器、 菜单控制器组和三个菜单项。

    ```xml
    <IDSymbol name="TestMenuController" value="0x1300" /><IDSymbol name="TestMenuControllerGroup" value="0x1060" /><IDSymbol name="cmdidMCItem1" value="0x0130" /><IDSymbol name="cmdidMCItem2" value="0x0131" /><IDSymbol name="cmdidMCItem3" value="0x0132" />
    ```

3. 菜单部分中的最后一个菜单项之后, 定义为菜单的菜单控制器。

    ```xml
    <Menu guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" priority="0x0100" type="MenuController">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <CommandFlag>IconAndText</CommandFlag>
        <CommandFlag>TextChanges</CommandFlag>
        <CommandFlag>TextIsAnchorCommand</CommandFlag>
        <Strings>
            <ButtonText>Test Menu Controller</ButtonText>
            <CommandName>Test Menu Controller</CommandName>
        </Strings>
    </Menu>
    ```

    `TextChanges`和`TextIsAnchorCommand`标志必须为包括在内，以启用菜单控制器，以反映所选的最后一个命令。

4. 在组部分，最后一个组条目后, 添加菜单控制器组。

    ```xml
    <Group guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" priority="0x000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" />
    </Group>
    ```

    通过设置与父菜单控制器，此组中置于任何命令显示在菜单控制器。 `priority`省略属性，其中将其设置为默认值 0，因为它是菜单控制器上的唯一组。

5. 在按钮部分中之后的最后一个按钮条目中，, 为每个菜单项添加一个按钮元素。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem1" priority="0x0000" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 1</ButtonText>
            <CommandName>MC Item 1</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem2" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 2</ButtonText>
            <CommandName>MC Item 2</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem3" priority="0x0200" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPicSearch" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 3</ButtonText>
            <CommandName>MC Item 3</CommandName>
        </Strings>
    </Button>
    ```

6. 此时，您可以查看菜单控制器。 生成项目并启动调试。 应会看到的实验实例。

   1. 上**视图 / 其他 Windows**菜单中，打开**测试 ToolWindow**。

   2. 在工具窗口的工具栏上显示菜单控制器。

   3. 单击以查看可能的三个命令的菜单控制器右侧的箭头。

      请注意，当您单击的命令，菜单控制器的标题更改以显示该命令。 在下一部分中，我们将添加代码以激活这些命令。

## <a name="implement-the-menu-controller-commands"></a>实现菜单控制器命令

1. 在中*TWTestCommandPackageGuids.cs*，现有的命令 Id 后添加三个菜单项的命令 Id。

    ```csharp
    public const int cmdidMCItem1 = 0x130;
    public const int cmdidMCItem2 = 0x131;
    public const int cmdidMCItem3 = 0x132;
    ```

2. 在中*TWTestCommand.cs*，在顶部添加以下代码`TWTestCommand`类。

    ```csharp
    private int currentMCCommand; // The currently selected menu controller command
    ```

3. TWTestCommand 构造函数，在最后一个调用中`AddCommand`方法中，添加代码以将每个命令通过同一处理程序的事件路由。

    ```csharp
    for (int i = TWTestCommandPackageGuids.cmdidMCItem1; i <=
        TWTestCommandPackageGuids.cmdidMCItem3; i++)
    {
        CommandID cmdID = new
        CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), i);
        OleMenuCommand mc = new OleMenuCommand(new
          EventHandler(OnMCItemClicked), cmdID);
        mc.BeforeQueryStatus += new EventHandler(OnMCItemQueryStatus);
        commandService.AddCommand(mc);
        // The first item is, by default, checked. 
        if (TWTestCommandPackageGuids.cmdidMCItem1 == i)
        {
            mc.Checked = true;
            this.currentMCCommand = i;
        }
    }
    ```

4. 添加到事件处理程序**TWTestCommand**类，以将标记为已检查所选的命令。

    ```csharp
    private void OnMCItemQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            mc.Checked = (mc.CommandID.ID == this.currentMCCommand);
        }
    }
    ```

5. 添加的事件处理程序显示一个 MessageBox，当用户选择菜单控制器上的命令：

    ```csharp
    private void OnMCItemClicked(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            string selection;
            switch (mc.CommandID.ID)
            {
                case c.cmdidMCItem1:
                    selection = "Menu controller Item 1";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem2:
                    selection = "Menu controller Item 2";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem3:
                    selection = "Menu controller Item 3";
                    break;

                default:
                    selection = "Unknown command";
                    break;
            }
            this.currentMCCommand = mc.CommandID.ID;

            IVsUIShell uiShell =
              (IVsUIShell) ServiceProvider.GetService(typeof(SVsUIShell));
            Guid clsid = Guid.Empty;
            int result;
            uiShell.ShowMessageBox(
                    0,
                    ref clsid,
                    "Test Tool Window Toolbar Package",
                    string.Format(CultureInfo.CurrentCulture,
                                 "You selected {0}", selection),
                    string.Empty,
                    0,
                    OLEMSGBUTTON.OLEMSGBUTTON_OK,
                    OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
                    OLEMSGICON.OLEMSGICON_INFO,
                    0,
                    out result);
        }
    }
    ```

## <a name="testing-the-menu-controller"></a>测试菜单控制器

1. 生成项目并启动调试。 应会看到的实验实例。

2. 打开**测试 ToolWindow**上**视图 / 其他 Windows**菜单。

    菜单控制器中的工具窗口的工具栏中将出现并显示**MC 项 1**。

3. 单击箭头左侧的菜单控制器按钮。

    应会看到三个项，其中第一个已选中，并有其图标周围突出显示的框。 单击**MC 项 3**。

    与消息会出现一个对话框**选择菜单控制器项 3**。 请注意，该消息对应于菜单控制器按钮上的文本。 菜单控制器按钮现在将显示**MC 项 3**。

## <a name="see-also"></a>请参阅
- [将工具栏添加到工具窗口](../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [添加工具栏](../extensibility/adding-a-toolbar.md)
