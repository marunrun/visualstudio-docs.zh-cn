---
title: 将工具栏添加到工具窗口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, adding toolbars
- toolbars [Visual Studio], adding to tool windows
ms.assetid: 172f64b3-87f8-4292-9c1c-65bffa2b0970
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bd4f4d37af94ba3a7dcdffc249e8b5e681025b78
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352396"
---
# <a name="add-a-toolbar-to-a-tool-window"></a>将工具栏添加到工具窗口
本演练演示如何将工具栏添加到工具窗口。

 工具栏是水平或垂直条包含绑定到命令的按钮。 工具窗口中工具栏的长度始终是相同的宽度或高度的工具窗口中，具体取决于工具栏的停靠位置。

 与在 IDE 中的工具栏，不同的工具窗口中的工具栏必须停靠和不能移动或自定义。 如果 VSPackage 在非代码中编写的在工具栏可停靠在任何边缘停靠。

 有关如何添加工具栏的详细信息，请参阅[将工具栏添加](../extensibility/adding-a-toolbar.md)。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-toolbar-for-a-tool-window"></a>创建工具窗口工具栏

1. 创建一个名为的 VSIX 项目`TWToolbar`具有名为这两个菜单命令**TWTestCommand**和名为工具窗口**TestToolWindow**。 有关详细信息，请参阅[与菜单命令创建一个扩展](../extensibility/creating-an-extension-with-a-menu-command.md)并[与工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。 您需要添加工具窗口模板之前添加命令项模板。

2. 在中*TWTestCommandPackage.vsct*，查找符号部分。 在名为 guidTWTestCommandPackageCmdSet GuidSymbol 节点声明一个工具栏和工具栏组，如下所示。

    ```xml
    <IDSymbol name="TWToolbar" value="0x1000" />
    <IDSymbol name="TWToolbarGroup" value="0x1050" />
    ```

3. 在顶部`Commands`部分中，创建`Menus`部分。 添加`Menu`元素来定义工具栏。

    ```xml
    <Menus>
        <Menu guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" type="ToolWindowToolbar">
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

     不能像子菜单嵌套工具栏。 因此，您无需指定一个父级。 此外，您无需设置优先级，因为用户可以移动工具栏。 通常情况下，初始放置工具栏的定义以编程方式，但用户的后续更改永久保存。

4. 在组部分中，定义一个组，包含工具栏的命令。

    ```xml

    <Group guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" priority="0x0000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" />
    </Group>
    ```

5. 在按钮部分中，将更改现有 Button 元素的父级为工具栏组，以便将显示工具栏。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="TWTestCommandId" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke TWTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     默认情况下，如果一个工具栏不具有任何命令，它不会不显示。

     因为新的工具栏不自动添加到工具窗口中，必须显式添加工具栏。 下一节中将对此进行讨论。

## <a name="add-the-toolbar-to-the-tool-window"></a>将工具栏添加到工具窗口

1. 在中*TWTestCommandPackageGuids.cs*添加以下行。

    ```csharp
    public const string guidTWTestCommandPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const int TWToolbar = 0x1000;
    ```

2. 在中*TestToolWindow.cs*添加以下 using 语句。

    ```csharp
    using System.ComponentModel.Design;
    ```

3. TestToolWindow 构造函数中添加以下行。

    ```csharp
    this.ToolBar = new CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), TWTestCommandPackageGuids.TWToolbar);
    ```

## <a name="test-the-toolbar-in-the-tool-window"></a>工具窗口中的测试工具栏

1. 生成项目并启动调试。 应显示 Visual Studio 实验实例。

2. 上**视图 / 其他 Windows**菜单上，单击**测试 ToolWindow**显示工具窗口。

     您应看到顶部的工具栏 （看起来像默认图标） 左侧的工具窗口标题的下方。

3. 在工具栏上，单击图标以显示消息**TWTestCommandPackage 内 TWToolbar.TWTestCommand.MenuItemCallback()** 。

## <a name="see-also"></a>请参阅
- [添加工具栏](../extensibility/adding-a-toolbar.md)