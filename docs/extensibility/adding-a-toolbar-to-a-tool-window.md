---
title: 向工具窗口添加工具栏 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tool windows, adding toolbars
- toolbars [Visual Studio], adding to tool windows
ms.assetid: 172f64b3-87f8-4292-9c1c-65bffa2b0970
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e5351fe6a713c217f8fca20d6740b542dc75f053
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85904121"
---
# <a name="add-a-toolbar-to-a-tool-window"></a>将工具栏添加到工具窗口
本演练演示如何将工具栏添加到工具窗口。

 工具栏是包含绑定到命令的按钮的水平或垂直条带。 工具窗口中工具栏的长度始终与工具窗口的宽度或高度相同，具体取决于工具栏的停靠位置。

 与 IDE 中的工具栏不同，工具窗口中的工具栏必须停靠并且无法移动或自定义。 如果 VSPackage 是用 umanaged 代码编写的，则可以在任何边缘停靠工具栏。

 有关如何添加工具栏的详细信息，请参阅 [添加工具栏](../extensibility/adding-a-toolbar.md)。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-toolbar-for-a-tool-window"></a>为工具窗口创建工具栏

1. 创建一个名为的 VSIX 项目 `TWToolbar` ，该项目包含一个名为 **TWTestCommand** 的菜单命令和一个名为 **TestToolWindow**的工具窗口。 有关详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md) 和 [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。 在添加工具窗口模板之前，需要添加命令项模板。

2. 在 *TWTestCommandPackage .vsct*中，查找 "符号" 部分。 在名为 guidTWTestCommandPackageCmdSet 的 GuidSymbol 节点中，按如下所示声明工具栏和工具栏组。

    ```xml
    <IDSymbol name="TWToolbar" value="0x1000" />
    <IDSymbol name="TWToolbarGroup" value="0x1050" />
    ```

3. 在部分的顶部 `Commands` ，创建一个 `Menus` 节。 添加 `Menu` 元素以定义工具栏。

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

     不能嵌套工具栏，如子菜单。 因此，您无需分配父级。 而且，您不必设置优先级，因为用户可以移动工具栏。 通常，将以编程方式定义工具栏的初始位置，但会保留用户的后续更改。

4. 在 "组" 部分中，定义一个包含工具栏命令的组。

    ```xml

    <Group guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" priority="0x0000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" />
    </Group>
    ```

5. 在 "按钮" 部分中，将 "现有 Button 元素" 的父项更改为工具栏组，以便显示工具栏。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="TWTestCommandId" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke TWTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     默认情况下，如果工具栏不包含命令，则它不会显示。

     由于新工具栏不会自动添加到工具窗口，因此必须显式添加工具栏。 下一节中将对此进行讨论。

## <a name="add-the-toolbar-to-the-tool-window"></a>将工具栏添加到工具窗口

1. 在 *TWTestCommandPackageGuids.cs* 中，添加以下行。

    ```csharp
    public const string guidTWTestCommandPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const int TWToolbar = 0x1000;
    ```

2. 在 *TestToolWindow.cs* 中，添加以下 using 语句。

    ```csharp
    using System.ComponentModel.Design;
    ```

3. 在 TestToolWindow 构造函数中，添加以下行。

    ```csharp
    this.ToolBar = new CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), TWTestCommandPackageGuids.TWToolbar);
    ```

## <a name="test-the-toolbar-in-the-tool-window"></a>测试工具窗口中的工具栏

1. 生成项目并启动调试。 应显示 Visual Studio 实验实例。

2. 在 " **视图"/"其他窗口** " 菜单上，单击 " **测试 ToolWindow** " 以显示工具窗口。

     应该会看到一个工具栏， (它在工具窗口左上角的默认图标) ，就在标题的正下方。

3. 在工具栏上，单击 "TWTestCommandPackage" 图标以显示消息 " **内部的 TWToolbar. TWTestCommand. MenuItemCallback ( # B1 **"。

## <a name="see-also"></a>另请参阅
- [添加工具栏](../extensibility/adding-a-toolbar.md)
