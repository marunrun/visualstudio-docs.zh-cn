---
title: 将菜单控制器添加到工具栏 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: d4dcb9e51f6633476a8f0eadea30da513e5ef760
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740328"
---
# <a name="add-a-menu-controller-to-a-toolbar"></a>将菜单控制器添加到工具栏
本演练基于"[将工具栏添加到工具窗口](../extensibility/adding-a-toolbar-to-a-tool-window.md)演练"为基础，演示如何向工具窗口工具栏添加菜单控制器。 此处显示的步骤也可以应用于在["添加工具栏](../extensibility/adding-a-toolbar.md)演练"中创建的工具栏。

菜单控制器是拆分控件。 菜单控制器的左侧显示最后使用的命令，您可以通过单击该命令来运行它。 菜单控制器的右侧是一个箭头，单击时，将打开其他命令的列表。 单击列表中的命令时，该命令将运行，并替换菜单控制器左侧的命令。 这样，菜单控制器的操作就像一个命令按钮，该按钮始终显示列表中最后使用的命令。

菜单控制器可以出现在菜单上，但它们最常用于工具栏。

## <a name="prerequisites"></a>先决条件
从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-menu-controller"></a>创建菜单控制器

1. 按照将[工具栏添加到工具窗口](../extensibility/adding-a-toolbar-to-a-tool-window.md)中描述的过程来创建具有工具栏的工具窗口。

2. 在*TWTest命令包.vsct 中*，转到符号部分。 在名为**guidTWTestCommandPackageCmdSet**的 GuidSymbol 元素中，声明菜单控制器、菜单控制器组和三个菜单项。

    ```xml
    <IDSymbol name="TestMenuController" value="0x1300" /><IDSymbol name="TestMenuControllerGroup" value="0x1060" /><IDSymbol name="cmdidMCItem1" value="0x0130" /><IDSymbol name="cmdidMCItem2" value="0x0131" /><IDSymbol name="cmdidMCItem3" value="0x0132" />
    ```

3. 在"菜单"部分中，在最后一个菜单条目之后，将菜单控制器定义为菜单。

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

    必须`TextChanges`包含`TextIsAnchorCommand`和 标志才能使菜单控制器反映最后一个选定的命令。

4. 在最后一个组条目之后的"组"部分中，添加菜单控制器组。

    ```xml
    <Group guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" priority="0x000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" />
    </Group>
    ```

    通过将菜单控制器设置为父级，在此组中放置的任何命令都会显示在菜单控制器中。 省略`priority`该属性，该属性将其设置为默认值 0，因为它是菜单控制器上的唯一组。

5. 在最后一个按钮条目之后，在"按钮"部分中，为每个菜单项添加一个按钮元素。

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

6. 此时，您可以查看菜单控制器。 生成项目并启动调试。 您应该会看到实验实例。

   1. 在 **"查看/其他窗口"** 菜单上，打开 **"测试工具窗口**"。

   2. 菜单控制器将显示在工具窗口中的工具栏上。

   3. 单击菜单控制器右侧的箭头以查看三个可能的命令。

      请注意，当您单击命令时，菜单控制器的标题将更改以显示该命令。 在下一节中，我们将添加代码来激活这些命令。

## <a name="implement-the-menu-controller-commands"></a>实现菜单控制器命令

1. 在*TWTestCommandPackageGuids.cs*中，在现有命令指示后为三个菜单项添加命令。"选项"。

    ```csharp
    public const int cmdidMCItem1 = 0x130;
    public const int cmdidMCItem2 = 0x131;
    public const int cmdidMCItem3 = 0x132;
    ```

2. 在*TWTestCommand.cs*中，在`TWTestCommand`类的顶部添加以下代码。

    ```csharp
    private int currentMCCommand; // The currently selected menu controller command
    ```

3. 在 TWTestCommand 构造函数中，在上次调用`AddCommand`方法后，添加代码以通过相同的处理程序路由每个命令的事件。

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

4. 将事件处理程序添加到**TWTestCommand**类，将所选命令标记为已选中。

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

5. 添加在用户选择菜单控制器上的命令时显示 MessageBox 的事件处理程序：

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

1. 生成项目并启动调试。 您应该会看到实验实例。

2. 在 **"查看/其他窗口"** 菜单上打开**测试工具窗口**。

    菜单控制器显示在工具窗口中的工具栏中，并显示 MC**项目 1**。

3. 单击箭头左侧的菜单控制器按钮。

    您应该会看到三个项目，其中第一个项目被选中，并在其图标周围有一个突出显示框。 单击**MC 项目 3**。

    将显示一个对话框，其中包含 **"您选择菜单控制器项目 3**"。 请注意，该消息对应于菜单控制器按钮上的文本。 菜单控制器按钮现在显示**MC 项目 3**。

## <a name="see-also"></a>请参阅
- [向工具窗口添加工具栏](../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [添加工具栏](../extensibility/adding-a-toolbar.md)
