---
title: 向工具窗口添加工具栏 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, adding toolbars
- toolbars [Visual Studio], adding to tool windows
ms.assetid: 172f64b3-87f8-4292-9c1c-65bffa2b0970
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 094515eb94279623974bd7b55cc9923c49625a70
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740248"
---
# <a name="add-a-toolbar-to-a-tool-window"></a>向工具窗口添加工具栏
本演练演示如何向工具窗口添加工具栏。

 工具栏是一个水平或垂直条带，其中包含绑定到命令的按钮。 工具窗口中工具栏的长度始终与工具窗口的宽度或高度相同，具体取决于工具栏停靠的位置。

 与 IDE 中的工具栏不同，工具窗口中的工具栏必须停靠，并且不能移动或自定义。 如果 VSPackage 是用 u 托管代码编写的，工具栏可以停靠在任何边缘。

 有关如何添加工具栏的详细信息，请参阅[添加工具栏](../extensibility/adding-a-toolbar.md)。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-toolbar-for-a-tool-window"></a>为工具窗口创建工具栏

1. 创建一个名为 VSIX`TWToolbar`项目的 VSIX 项目，该项目具有名为**TWTestCommand**的菜单命令和名为**TestToolWindow**的工具窗口。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)，以及[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。 在添加工具窗口模板之前，需要添加命令项模板。

2. 在*TWTestCommandPackage.vsct 中*，查找符号部分。 在名为 guidTWTestCommandPackageCmdSet 的 GuidSymbol 节点中，声明工具栏和工具栏组，如下所示。

    ```xml
    <IDSymbol name="TWToolbar" value="0x1000" />
    <IDSymbol name="TWToolbarGroup" value="0x1050" />
    ```

3. 在`Commands`节的顶部，创建一个`Menus`节。 添加元素`Menu`以定义工具栏。

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

     工具栏不能像子菜单一样嵌套。 因此，您不必分配父级。 此外，您不必设置优先级，因为用户可以移动工具栏。 通常，工具栏的初始放置以编程方式定义，但用户的后续更改将保持不变。

4. 在"组"部分中，定义一个组以包含工具栏的命令。

    ```xml

    <Group guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" priority="0x0000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" />
    </Group>
    ```

5. 在"按钮"部分中，将现有 Button 元素的父元素更改为工具栏组，以便显示工具栏。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="TWTestCommandId" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke TWTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     默认情况下，如果工具栏没有命令，则不会显示。

     由于新工具栏不会自动添加到工具窗口，因此必须显式添加工具栏。 下一节中将对此进行讨论。

## <a name="add-the-toolbar-to-the-tool-window"></a>将工具栏添加到工具窗口

1. 在*TWTestCommandPackageGuids.cs*添加以下行。

    ```csharp
    public const string guidTWTestCommandPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const int TWToolbar = 0x1000;
    ```

2. 在*TestToolWindow.cs*添加以下 using 语句。

    ```csharp
    using System.ComponentModel.Design;
    ```

3. 在 TestToolWindow 构造函数中添加以下行。

    ```csharp
    this.ToolBar = new CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), TWTestCommandPackageGuids.TWToolbar);
    ```

## <a name="test-the-toolbar-in-the-tool-window"></a>在工具窗口中测试工具栏

1. 生成项目并启动调试。 应出现可视化工作室实验实例。

2. 在 **"查看/其他窗口"** 菜单上，单击 **"测试工具窗口**"以显示工具窗口。

     您应该在工具窗口的左上角看到一个工具栏（它看起来像默认图标），就在标题的正下方。

3. 在工具栏上，单击该图标以在**TWToolbar.TWTestCommand.Menu 项目回拨（） 中显示消息 TWTestCommandPackage。**

## <a name="see-also"></a>请参阅
- [添加工具栏](../extensibility/adding-a-toolbar.md)
