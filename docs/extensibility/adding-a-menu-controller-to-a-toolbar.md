---
title: 将菜单控制器添加到工具栏 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding menu controllers
- menus, adding menu controllers to toolbars
- menu controllers, adding to toolbars
ms.assetid: 6af9b0b4-037f-404c-bb40-aaa1970768ea
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 32cbbbc7784c112b33b5f720b306b8c93269bb82
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903529"
---
# <a name="add-a-menu-controller-to-a-toolbar"></a>向工具栏添加菜单控制器
本演练[以 "将工具栏添加到工具窗口](../extensibility/adding-a-toolbar-to-a-tool-window.md)" 演练为基础，并演示如何将菜单控制器添加到工具窗口工具栏中。 此处所示的步骤还可以应用于在 "[添加工具栏](../extensibility/adding-a-toolbar.md)" 演练中创建的工具栏。

菜单控制器是拆分控件。 菜单控制器左侧显示了上次使用的命令，你可以通过单击该命令来运行该命令。 菜单控制器的右侧是一个箭头，单击它将打开其他命令的列表。 单击该列表上的命令时，该命令将运行，并且它将替换菜单控制器左侧的命令。 这样，菜单控制器的工作方式类似于命令按钮，该按钮始终显示列表中最后使用的命令。

菜单控制器可以出现在菜单中，但它们最常在工具栏上使用。

## <a name="prerequisites"></a>必备条件
从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-menu-controller"></a>创建菜单控制器

1. 按照[将工具栏添加到工具窗口](../extensibility/adding-a-toolbar-to-a-tool-window.md)中所述的过程来创建具有工具栏的工具窗口。

2. 在*TWTestCommandPackage .vsct*中，请参阅符号部分。 在名为**guidTWTestCommandPackageCmdSet**的 GuidSymbol 元素中，声明菜单控制器、菜单控制器组和三个菜单项。

    ```xml
    <IDSymbol name="TestMenuController" value="0x1300" /><IDSymbol name="TestMenuControllerGroup" value="0x1060" /><IDSymbol name="cmdidMCItem1" value="0x0130" /><IDSymbol name="cmdidMCItem2" value="0x0131" /><IDSymbol name="cmdidMCItem3" value="0x0132" />
    ```

3. 在菜单部分中的最后一个菜单项后，将菜单控制器定义为菜单。

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

    `TextChanges` `TextIsAnchorCommand` 必须包含和标志才能使菜单控制器反映最后一次选定的命令。

4. 在 "组" 部分中的最后一个组条目后，添加菜单控制器组。

    ```xml
    <Group guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" priority="0x000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" />
    </Group>
    ```

    通过将菜单控制器设置为父项，放置在此组中的所有命令都将出现在菜单控制器中。 `priority`省略属性，这会将其设置为默认值0，因为它是菜单控制器上的唯一组。

5. 在 "按钮" 部分的最后一个按钮项后，为每个菜单项添加一个 Button 元素。

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

6. 此时，您可以查看菜单控制器。 生成项目并启动调试。 应会看到实验实例。

   1. 在 "**视图"/"其他窗口**" 菜单上，打开 "**测试 ToolWindow**"。

   2. 菜单控制器显示在工具窗口的工具栏中。

   3. 单击菜单控制器右侧的箭头，查看三个可能的命令。

      请注意，当您单击某个命令时，菜单控制器的标题将更改以显示该命令。 在下一部分中，我们将添加代码来激活这些命令。

## <a name="implement-the-menu-controller-commands"></a>实现菜单控制器命令

1. 在*TWTestCommandPackageGuids.cs*中，在现有的命令 id 后面添加三个菜单项的命令 id。

    ```csharp
    public const int cmdidMCItem1 = 0x130;
    public const int cmdidMCItem2 = 0x131;
    public const int cmdidMCItem3 = 0x132;
    ```

2. 在*TWTestCommand.cs*中，在类的顶部添加以下代码 `TWTestCommand` 。

    ```csharp
    private int currentMCCommand; // The currently selected menu controller command
    ```

3. 在 TWTestCommand 构造函数中，在最后一次调用 `AddCommand` 方法后，添加代码，以便通过相同的处理程序为每个命令路由事件。

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

4. 向**TWTestCommand**类添加一个事件处理程序，以将所选命令标记为已选中。

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

5. 添加一个事件处理程序，该处理程序在用户选择菜单控制器上的命令时显示 MessageBox：

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

1. 生成项目并启动调试。 应会看到实验实例。

2. 在 "视图"/"**其他窗口**" 菜单上打开 "**测试 ToolWindow** "。

    菜单控制器显示在工具窗口的工具栏中，并显示**MC 项 1**。

3. 单击箭头左侧的 "菜单控制器" 按钮。

    应会看到三个项，其中第一个项处于选中状态，并且其图标周围有一个突出显示框。 单击 " **MC 项目 3**"。

    此时将显示一个对话框，其中包含**所选的 "菜单控制器项 3**"。 请注意，该消息对应于菜单控制器按钮上的文本。 菜单控制器按钮现在显示**MC 项目 3**。

## <a name="see-also"></a>另请参阅
- [将工具栏添加到工具窗口](../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [添加工具栏](../extensibility/adding-a-toolbar.md)
